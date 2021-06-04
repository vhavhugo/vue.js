<template>
  <div>
    <h1>{{ titulo }}</h1>
      <ul>
        <li v-for="foto of fotos">
          <img :src="foto.url" :alt="foto.titulo">
        </li>
      </ul>
  </div>
</template>

<script>
export default {

  data() {

    return {

      titulo: 'Alurapic',
      fotos: [

      ]

    }

  },

  created() {
    alert('Criei o componentes');
  }
}
</script>

<style>

</style>
