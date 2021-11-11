<template>
  <div class="urna-tela">
    <div v-if="tela != 'fim'" class="urna-tela-voto">
      <div class="urna-tela-voto-textos">
        <div class="urna-tela-voto-titulo">Seu voto para:</div>

        <div class="urna-tela-voto-tipo">{{ tela }}</div>

        <div class="urna-tela-voto-numeros">
          Números
          <div
            class="urna-tela-voto-numero"
            v-for="(value, key) in numeroVoto.padEnd(quantidadeNumeros, ' ')"
            :key="key"
          >
            {{ value }}
          </div>
        </div>

        <div class="urna-tela-voto-descricao">
          Nome: <strong>{{ candidato.nome ? candidato.nome : "___________" }}</strong>
        </div>

        <div class="urna-tela-voto-descricao">
          Partido: <strong>{{ candidato.partido ? candidato.partido : "__________" }}</strong>
        </div>
      </div>

      <div class="urna-tela-voto-imagem"></div>

      <div class="urna-tela-voto-instrucoes"></div>
    </div>

    <div v-if="tela == 'fim'" class="urna-tela-fim">
      Finalização
    </div>
  </div>
</template>

<script>
export default {
  name: "Tela",
  props: {
    tela: String,
    numeroVoto: String,
    quantidadeNumeros: Number,
    candidato: Object
  }
};
</script>

<style>
.urna-tela {
  background-color: var(--ballot-box-screen-color);
  border: 2px solid var(--light-border-color);
  border-radius: 5px;
  color: var(--dark-text-color);
  height: 100%;
  padding: 20px;
  width: 55%;
}

.urna-tela-voto-titulo {
  font-size: 20px;
}

.urna-tela-voto-tipo {
  font-size: 30px;
  font-weight: bold;
  margin: 20px 0;
  text-transform: uppercase;
}

.urna-tela-voto-numeros {
  align-items: center;
  display: flex;
}

.urna-tela-voto-numero {
  align-items: center;
  border: 1px solid var(--dark-border-color);
  display: flex;
  font-size: 30px;
  justify-content: center;
  height: 55px;
  margin-left: 10px;
  width: 45px;
}
</style>
