<template>
  <div class="final">
    <div :class="`final-texto ${etapa}`">
      {{ texto }}
    </div>
    <button @click="reset" class="final-botao">Jogar novamente</button>
  </div>
</template>

<script>
export default {
  name: "Final",
  props: {
    etapa: String,
    texto: String,
    reset: Function
  },
}
</script>

<style scoped>
.final-texto {
  margin: 20px 0;
  font-size: 24px;
  font-weight: bold;
}

.final-texto.enforcado {
  color: var(--color-text-error)
}

.final-texto.ganhador {
  color: var(--color-text-success)
}
</style>
