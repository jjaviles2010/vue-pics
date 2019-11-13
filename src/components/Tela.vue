<template>
  <div>
    <h1>{{msg}}</h1>
    <h3 v-text="titulo + ' olá'"></h3>
    <button v-on:click="reverseMessage">Inverter</button>
    <p>{{message}}</p>

    <input v-model="message">
    
    <p v-text="titulo + new Date().toLocaleString()"></p>
    <span v-if="seen">Mostra isso?</span>
    <img v-bind:src="foto.url" v-bind:alt="foto.alt" />
    <ul>
      <li v-for="foto in fotos" :key="foto.id">
        <img v-bind:src="foto.url" :alt="foto.alt" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Tela",
  methods: {
      reverseMessage(){
         this.message = this.message.split('').reverse().join('')
      }
  },
  data() {
    return {
      seen: true,
      message: "Texto a ser invertido",
      titulo: "Titulo da minha pagina",
      foto: {
        url:
          "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
        alt: "Cachorro"
      },
      fotos: [
        {
          id: 0,
          url:
            "https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTwV4kVzT5McBdGSgqlVeRzubrNH_mOrrkKseDOGFURq20HmsrelEfMU7It",
          alt: "Cachorro"
        },
        {
          id: 1,
          url:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOhmlmzV4-Sifx5BIc2SXeA-1CtZJf8jb8V_vPZyKbXIQJKU-rkxGO6OM",
          alt: "Gato"
        }
      ]
    };
  },
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
