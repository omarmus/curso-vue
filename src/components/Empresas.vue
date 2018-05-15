<template>
  <section>
    <h2>Empresas</h2>
    <table>
      <tr>
        <th>Nombre</th>
        <th>Dirección</th>
      </tr>
      <tr v-for="item in empresas" :key="item.id">
        <td>{{ item.nombre }}</td>
        <td>{{ item.direccion }}</td>
      </tr>
    </table>
  </section>
</template>

<script>
import axios from 'axios'
const url = 'http://localhost:4000/api-rest/empresas';

export default {
  created () {
    axios.get(url)
    .then((respuesta) => {
      console.log(respuesta.data)
      this.empresas = respuesta.data
      console.log(this.empresas)
    })
  },
  data () {
    return {
      empresas: []
    }
  }
}
</script>
