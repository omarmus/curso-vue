<template>
  <section>
    <h2>Empresas</h2>
    <form @submit="agregar">
      Nombre: <input type="text" v-model="nombre"> <br>
      Dirección: <input type="text" v-model="direccion"> <br>
      <button type="button">Cancelar</button>
      <button type="submit">Agregar</button>
    </form>
    <table>
      <tr>
        <th>Nombre</th>
        <th>Dirección</th>
        <th>Acciones</th>
      </tr>
      <tr v-for="item in empresas" :key="item.id">
        <td>{{ item.nombre }}</td>
        <td>{{ item.direccion }}</td>
        <td>
          <button type="button" @click="eliminar(item.id)">Eliminar</button>
        </td>
      </tr>
    </table>
  </section>
</template>

<script>
import axios from 'axios'
const url = 'http://localhost:4000/api-rest/empresas';

export default {
  created () {
    this.lista()
  },
  data () {
    return {
      empresas: [],
      nombre: '',
      direccion: ''
    }
  },
  methods: {
    agregar () {
      console.log(this.nombre, this.direccion)
      const data = {
        nombre: this.nombre,
        direccion: this.direccion
      }
      axios.post(url, data)
      .then(respuesta => {
        console.log(respuesta)
        this.lista()
      })
    },
    lista () {
      axios.get(url)
      .then((respuesta) => {
        console.log(respuesta.data)
        this.empresas = respuesta.data
        console.log(this.empresas)
      })
    },
    eliminar (id) {
      if (confirm('¿Eliminar?')) {
        axios.delete(`${url}/${id}`) // url + '/' + id
        .then(respuesta => {
          this.lista()
        })
      }
    }
  }
}
</script>
