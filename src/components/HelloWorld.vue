<template>
  <section>
    <h1>{{ mensaje }}</h1>
    <input type="text" v-model="mensaje"><br>
    Número: <input type="text" v-model="numero">
    <button v-on:click="agregar()">Agregar</button>
    <button @click="sumar">Sumar números</button>
    <h3>Resultado: {{ resultado }}</h3>
    <ul v-if="lista.length > 0">
      <li>Lista</li>
      <li v-for="item in lista" :key="item">{{ item }}</li>
    </ul>
    <h4 v-else>Lista vacia</h4>
    <hr>
    <table>
      <tr>
        <th>Nombre</th>
        <th>Email</th>
      </tr>
      <tr v-for="item in usuarios" :key="item.id">
        <td>{{ item.name }}</td>
        <td>{{ item.email }}</td>
      </tr>
    </table>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  created () {
    const url = 'https://jsonplaceholder.typicode.com/users';

    axios.get(url)
    .then(respuesta => {
      console.log(respuesta.data)
      this.usuarios = respuesta.data
    })
  },
  mounted () {

  },
  data () {
    return {
      mensaje: 'Hola mundo',
      lista: [],
      numero: '',
      resultado: '',
      usuarios: []
    }
  },
  methods: {
    agregar () {
      console.log(this.numero)
      this.lista.push(this.numero)
    },
    sumar () {
      let suma = 0
      for (let i in this.lista) {
        suma += parseInt(this.lista[i])
      }
      this.resultado = suma
    }
  }
}
</script>