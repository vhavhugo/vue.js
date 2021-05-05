<template>
<div>
  <h1>{{ titulo }}</h1>
  <ul>
    <li v-for="foto of fotos">
      <img :src="foto.url" :alt="foto.titulo"/>
    </li>
  </ul>
</div>
</template>

<script>
export default {
  data(){
    return{
      titulo: 'Alurapic',
      fotos: [
        {
          url: 'https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.F4C7GmtZcmeDikxFHIx02QHaFj%26pid%3DApi%26h%3D160&f=1',
          titulo: "cachorro"
        },
        {
        url: 'https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.Jf0NnGpH2AhNM3BtwZufwwHaJ4%26pid%3DApi%26h%3D160&f=1',
        titulo: "cachorrão"
      }]
    }
  }
}
</script>

<style>

</style>
