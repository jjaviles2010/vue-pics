<template>
  <div class="corpo">
    <h1 class="centralizado">{{msg}}</h1>
    <h3 v-text="titulo + ' olá'"></h3>
    <button v-on:click="reverseMessage">Inverter</button>
    <p>{{message}}</p>

    <input v-model="message" />

    <p v-text="titulo + new Date().toLocaleString()"></p>
    <span v-if="seen">Mostra isso?</span>
    <img v-bind:src="foto.url" v-bind:alt="foto.alt" />
    <ul class="lista-fotos">
      <li v-for="user in users" :key="user.id" class="lista-fotos-item">
        <div class="painel">
          <h2 class="painel-titulo">{{user.first_name + ' ' + user.last_name}}</h2>
          <div class="painel-corpo">
            <img
              class="imagem-responsivas"
              v-bind:src="user.avatar"
              :alt="user.first_name"
              :title="user.first_name + user.last_name"
            />
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Tela",
  created() {
    axios
      .get("https://reqres.in/api/users")
      .then(response => {
        this.users = response.data.data;
      })
      .catch(erro => {
        this.erros.push(erro);
      });
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split("")
        .reverse()
        .join("");
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
      ],
      users: [],
      erros: []
    };
  },
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.centralizado {
  text-align: center;
}

.corpo {
  font-family: Helvetica, Arial, sans-serif;
  margin: 0 auto;
  width: 96%;
  color: gray;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

/* estilo do painel */

.imagem-responsiva {
    width: 100%;
  }

.painel {
  padding: 0 auto;
  border: solid 1px grey;
  display: inline-block;
  margin: 0 10px;
  box-shadow: 2px 2px 10px grey;
  width: 150px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}

.painel .painel-titulo {
  font-size: 14px;
  text-align: center;
  border-bottom: solid 1px grey;
  background: mediumspringgreen;
  margin: 0;
  padding: 10px;
  text-transform: uppercase;

}
</style>
