<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <button :disabled="ativo" class="button" @click="iniciar">
      <span class="icon">
        <i class="fas fa-play"> </i>
      </span>
      <span>Play</span>
    </button>
    <button :disabled="!ativo" class="button" @click="finalizar">
      <span class="icon">
        <i class="fas fa-stop"> </i>
      </span>
      <span>Stop</span>
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";

export default defineComponent({
  name: "Temporizador",
  data() {
    return { tempoEmSegundos: 0, ativo: false, cronometro: 0 };
  },
  methods: {
    iniciar() {
      this.ativo = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizar() {
      this.ativo = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
  emits: ["aoTemporizadorFinalizado"],
  components: { Cronometro },
});
</script>

<style></style>
