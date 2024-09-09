<template>
  <div class="palavra">
    <div class="palavra-letras">
      <div v-for="(letra, index) in palavra" :key="index" class="palavra-letra">
        {{ (verificarLetra(letra) || etapa === 'enforcado') ? letra : '' }}
      </div>
    </div>

    <div class="palavra-dica">
      {{ dica }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Palavra",
  props: {
    erros: Number,
    palavra: String,
    dica: String,
    verificarLetra: Function,
    etapa: String
  },
}
</script>

<style scoped>
.palavra {
  text-transform: uppercase;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.palavra-letras {
  display: flex;
  margin-bottom: 20px;
}

.palavra-letra {
  height: 30px;
  width: 30px;
  margin: 0 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid var(--color-text-light);
}
</style>
