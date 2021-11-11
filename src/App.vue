<template>
  <div id="app">
    <div class="urna">
      <Tela
        :tela="tela"
        :numeroVoto="numeroVoto"
        :quantidadeNumeros="quantidadeNumeros"
        :candidato="candidato"
      />
      <Teclado :adicionarNumero="adicionarNumero" :corrigir="corrigir" />
    </div>
  </div>
</template>

<script>
import "./css/global.css";
import Teclado from "./components/Teclado.vue";
import Tela from "./components/Tela.vue";

export default {
  name: "app",
  components: {
    Teclado,
    Tela
  },
  methods: {
    adicionarNumero(numero) {
      // verificar o limite de numeros votados
      if (this.numeroVoto.length == this.quantidadeNumeros) {
        return false;
      }

      // adiciona o numero selecionado
      this.numeroVoto += "" + numero;

      // verifica o candidato votado
      this.verificarCandidato();
    },
    verificarCandidato() {
      // voto incompleto
      if (this.numeroVoto.length < this.quantidadeNumeros) {
        return false;
      }

      // verifica se existe um candidato
      if (this.candidatos[this.tela][this.numeroVoto]) {
        this.candidato = this.candidatos[this.tela][this.numeroVoto];
        return true;
      }

      // voto nulo
      this.candidato = {
        nome: "Voto nulo",
        partido: "Voto nulo",
        imagem: ""
      };
    },
    corrigir() {
      this.limpar();
    },
    limpar() {
      this.candidato = {}
      this.numeroVoto = ''
    }
  },
  data() {
    return {
      tela: "prefeito",
      numeroVoto: "",
      quantidadeNumeros: 2,
      candidato: {},
      candidatos: {
        prefeito: {
          "01": {
            nome: "Ash",
            partido: "Pokemon",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/ash.png"
          },
          "08": {
            nome: "Vegeta",
            partido: "Dragon Ball",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/vegeta.png"
          }
        },
        vereador: {
          "01234": {
            nome: "Pikachu",
            partido: "Pokemon",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/pikachu.png"
          },
          "08001": {
            nome: "Goku",
            partido: "Dragon Ball",
            imagem:
              "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/goku.png"
          }
        }
      }
    };
  }
};
</script>

<style>
#app {
  align-items: center;
  background-color: var(--background-color);
  display: flex;
  justify-content: center;
  height: 100%;
  width: 100%;
}

.urna {
  background-color: var(--ballot-box-background-color);
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  height: 500px;
  padding: 30px;
  width: 1000px;
}
</style>
