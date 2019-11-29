<template>
  <div class="corpo">
    <h1 class="centralizado">{{msg}}</h1>
    <input v-on:input="filtro = $event.target.value" type="search" placeholder="filtre pelo primeiro nome" class="filtro" />
    <ul class="lista-fotos">
      <li v-for="user in fotosComFiltro" :key="user.id" class="lista-fotos-item">
          <meu-painel v-bind:titulo="user.first_name + ' ' + user.last_name">
            <img class="imagem-resposiva" :src="user.avatar" :alt="user.first_name" :title="user.first_name + ' ' + user.last_name" />
          </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Painel from "./shared/Painel";
export default {
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), "i");
        return this.users.filter(user => exp.test(user.first_name))

      } else {
        return this.users;
      }
    }
  },
  components: {
    "meu-painel": Painel
  },
  name: "Tela",
  created() {
    axios
      .get("https://reqres.in/api/users")
      .then(response => {
        this.users = response.data.data;
      }).catch(erro => {
        this.erros.push(erro)
      })
  },
  methods: {
      reverseMessage(){
          this.message = this.message.split('').reverse().join('');
      }
  },
  data() {
    return {
      titulo: "Título da minha página",
      seen: false,
      message: "Texto a ser invertido",
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
      erros:[],
      filtro: "",
    };
  },
  props: {
    msg: String
  }
};
</script>

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

.filtro {
  display: block;
  width: 80%;
  height: 44px;
  padding: 5px;
  font-size: 16px;
}

</style>
