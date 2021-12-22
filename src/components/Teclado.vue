<template>
  <div class="urna-teclado">
    <div class="urna-teclado-numerico">
      <div class="urna-teclado-numerico-linha">
        <button v-on:click="adicionarNumero(1)">1</button>
        <button v-on:click="adicionarNumero(2)">2</button>
        <button v-on:click="adicionarNumero(3)">3</button>
      </div>

      <div class="urna-teclado-numerico-linha">
        <button v-on:click="adicionarNumero(4)">4</button>
        <button v-on:click="adicionarNumero(5)">5</button>
        <button v-on:click="adicionarNumero(6)">6</button>
      </div>

      <div class="urna-teclado-numerico-linha">
        <button v-on:click="adicionarNumero(7)">7</button>
        <button v-on:click="adicionarNumero(8)">8</button>
        <button v-on:click="adicionarNumero(9)">9</button>
      </div>

      <div class="urna-teclado-numerico-linha">
        <button v-on:click="adicionarNumero(0)">0</button>
      </div>
    </div>

    <div class="urna-teclado-acoes">
      <button class="btn-branco" v-on:click="votarEmBranco()">Branco</button>
      <button class="btn-corrige" v-on:click="corrigir()">Corrige</button>
      <button class="btn-confirma" v-on:click="confirmar()">Confirma</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Teclado",
  props: {
    adicionarNumero: Function,
    corrigir: Function,
    confirmar: Function,
    votarEmBranco: Function
  }
};
</script>

<style>
.urna-teclado{
  background-color: var(--ballot-box-keyboard-color);
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 100%;
  padding: 20px;
  width: 40%;
}
.urna-teclado-numerico{
  width: 100%;
}

.urna-teclado-numerico-linha{
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.urna-teclado-numerico-linha button{
  background-color: var(--ballot-box-keyboard-button-color);
  border-radius: 5px;
  color: var(--light-text-color);
  font-size: 30px;
  height: 50px;
  width: 80px;
}

.urna-teclado-acoes{
  display: flex;
  justify-content: space-around;
  width: 100%;
}

.urna-teclado-acoes button{
  border-radius: 5px;
  color: var(--dark-text-color);
  font-size: 15px;
  height: 50px;
  text-transform: uppercase;
  width: 30%;
}

.btn-branco{
  background-color: var(--ballot-box-white-button-color);
}

.btn-corrige{
  background-color: var(--ballot-box-correct-button-color);
}

.btn-confirma{
  background-color: var(--ballot-box-confirm-button-color);
}
</style>
