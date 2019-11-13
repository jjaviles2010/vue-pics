<template>
<div>
    <h1>{{msg}}</h1>
    <h3 v-text="titulo + ' olá'"></h3>
    <p v-text="titulo + new Date().toLocaleString()"></p>
    <span v-if="seen">Mostra isso?</span>
    <img v-bind:src="foto.url" v-bind:alt="foto.alt">
</div>
</template>

<script>
export default {
  name: "Tela",
  data(){
      return {
          seen: true,
          titulo: "Titulo da minha pagina",
          foto: {
              url: "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
              alt: "Cachorro"
          }
      }
  },
  props: {
      msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
