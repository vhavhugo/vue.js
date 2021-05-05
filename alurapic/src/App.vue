<template>
<div>
  <h1>{{ titulo }}</h1>
  <img :src="foto.url" :alt="foto.titulo"/>
</div>
</template>

<script>
export default {
  data(){
    return{
      titulo: 'Alurapic',
      foto: {
        url: 'https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.F4C7GmtZcmeDikxFHIx02QHaFj%26pid%3DApi%26h%3D160&f=1',
        titulo: "cachorro"
      }
    }
  }
}
</script>

<style>

</style>
