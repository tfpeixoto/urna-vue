<template>
  <div id="app">
    <div class="urna">
      <Tela
        :tela="tela"
        :numeroVoto="numeroVoto"
        :quantidadeNumeros="quantidadeNumeros"
        :candidato="candidato"
      />
      <Teclado
        :adicionarNumero="adicionarNumero"
        :corrigir="corrigir"
        :confirmar="confirmar"
        :votarEmBranco="votarEmBranco"
      />
    </div>
  </div>
</template>

<script>
import "./css/global.css";
import Teclado from "./components/Teclado.vue";
import Tela from "./components/Tela.vue";
// import confirmAudio from "@/assets/audios/confirm.wav";
// import keyAudio from "@/assets/audios/key.wav";

export default {
  name: "app",
  components: {
    Teclado,
    Tela
  },

  methods: {
    adicionarNumero(numero) {
      // tocar som
      // this.executarSom(keyAudio);

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

      // tocar som
      // this.executarSom(keyAudio);
    },

    limpar() {
      this.candidato = {};
      this.numeroVoto = "";
    },

    confirmar() {
      if (this.numeroVoto.length < this.quantidadeNumeros) {
        return false;
      }

      return this.avancarTela();
    },

    avancarTela() {
      // vereador
      if (this.tela == "prefeito") {
        this.tela = "vereador";
        this.quantidadeNumeros = 5;
        return this.limpar();
      }

      // tocar som
      // this.executarSom(confirmAudio);

      // finalização
      this.tela = "fim";

      // instância atual
      var instancia = this;

      // voltar ao início
      setTimeout(function(){
        instancia.tela = 'prefeito';
        instancia.quantidadeNumeros = 2;
        return instancia.limpar();
      }, 3000)
    },

    votarEmBranco() {
      if(this.tela == 'fim'){
        return false;
      }

      this.limpar();
      this.avancarTela();
    },

    // executarSom(arquivoSom){
    //   if(arquivoSom){
    //     let audio = new Audio(arquivoSom);
    //     audio.play();
    //   }
    // }
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
