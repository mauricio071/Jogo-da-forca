<template>
  <div class="formulario">

    <div class="formulario-title">{{ title }}</div>

    <input v-model="inputValue" type="text" class="formulario-input">

    <button
      @click="onSubmit"
      :disabled="inputValue.length === 0">{{ button }}
    </button>
  </div>
</template>

<script>
export default {
  name: "Formulario",
  props: {
    title: String,
    button: String,
    action: Function
  },
  data() {
    return {
      inputValue: '',
    }
  },
  methods: {
    onSubmit() {
      this.action(this.inputValue)
      this.inputValue = ''
    }
  },
}
</script>

<style scoped>
.formulario {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.formulario-input {
  padding: 10px 5px;
  margin: 10px 0;
  border: 0;
  border-radius: 5px;
  text-align: center;
  color: var(--color-text-dark);
  font-size: 16px;
}
</style>
