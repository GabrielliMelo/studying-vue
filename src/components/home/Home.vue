<template>
  <div>
    <h1 class="centralizado">VUE</h1>
    <input
      type="search"
      class="filtro"
      @input="filtro = $event.target.value"
      placeholder="filtre pelo título da foto"
    />
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <!-- componente sendo usado e passando via props conteudo !! -->
        <meu-painel
          v-meu-transform:teste.animate.reverse="15"
          :titulo="foto.titulo"
          :texto="mensagem"
        >
          <!-- <imagem-responsiva
            :url="foto.url"
            :titulo="foto.titulo"
            v-meu-transform:rotate.animate="30"
          /> -->
          <imagem-responsiva
            :url="foto.url"
            :titulo="foto.titulo"
            v-meu-transform:scale.animate="1.2"
          />
          <meu-botao
            rotulo="remover"
            tipo="button"
            @botaoAtivado="remove(foto)"
            :confirmacao="true"
            estilo="padrao"
          />
        </meu-painel>
      </li>
    </ul>
    <input
      type="search"
      class="filtro"
      @input="Nome = $event.target.value"
      placeholder="Digite o seu nome"
    />
  </div>
</template>

<script>
//importando o componente
import Painel from "../shared/painel/Painel.vue";
import ImagemResponsiva from "../shared/imagem-responsiva/imagemResponsiva.vue";
import Botao from "../shared/botao/Botao.vue";

export default {
  //declarando meu componente para usar no template
  components: {
    "meu-painel": Painel,
    "imagem-responsiva": ImagemResponsiva,
    "meu-botao": Botao
  },

  data() {
    return {
      titulo: "Estudando Vue.js",

      fotos: [],

      filtro: "",
      Nome: ""
    };
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), "i"); //sensitive...
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    },
    mensagem() {
      return "Bem vindo(a)," + this.Nome;
    }
  },

  created() {
    this.$http
      .get("http://localhost:3000/v1/fotos")
      .then(res => res.json())
      .then(
        fotos => (this.fotos = fotos),
        err => console.log(err)
      );
  },
  methods: {
    remove(foto) {
      alert("remover foto: " + foto.titulo);
    }
  }
};
</script>
<style>
.centralizado {
  text-align: center;
}

.lista-fotos {
  list-style: none;
}

.lista-fotos .lista-fotos-item {
  display: inline-block;
}

.imagem-responsiva {
  width: 100%;
}

.filtro {
  display: block;
  width: 100%;
}
</style>
