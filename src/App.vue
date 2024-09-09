<template>
  <div id="app">
    <h1>Jogo da forca</h1>

    <section v-if="tela === 'inicio'" id="inicio">
      <Formulario v-if="etapa === 'palavra'" title="Defina a palavra" button="Próximo" :action="setPalavra" />

      <Formulario v-if="etapa === 'dica'" title="Defina a dica" button="Inicar jogo :)" :action="setDica" />
    </section>

    <section v-if="tela === 'jogo'" id="Jogo">
      <Jogo :erros="erros" :palavra="palavra" :dica="dica" :verificarLetra="verificarLetra" :etapa="etapa"
        :letras="letras" :jogar="jogar" :reset="reset" />
    </section>
  </div>
</template>

<script>
import './css/global.css';
import Formulario from './components/Formulario.vue'
import Jogo from './components/Jogo.vue'
export default {
  name: 'App',
  data() {
    return {
      tela: 'inicio',
      etapa: 'palavra',
      palavra: '',
      dica: '',
      erros: 0,
      letras: []
    }
  },
  components: {
    Formulario,
    Jogo
  },
  methods: {
    setPalavra(palavra) {
      this.palavra = palavra;
      this.etapa = 'dica';
    },

    setDica(dica) {
      this.dica = dica;
      this.tela = 'jogo';
      this.etapa = 'jogo';
    },

    verificarLetra(letra) {
      return this.letras.find(item => item.toLowerCase() === letra.toLowerCase())
    },

    jogar(letra) {
      this.letras.push(letra)

      this.verificarErros(letra)
    },

    verificarErros(letra) {
      if (this.palavra.toLowerCase().indexOf(letra.toLowerCase()) >= 0) {
        return this.verificarAcertos();
      }

      this.erros++

      if (this.erros === 6) {
        this.etapa = 'enforcado'
      }
    },

    verificarAcertos() {
      let letrasUnicas = [...new Set(this.palavra.toLowerCase().split(''))]
      if (letrasUnicas.length === (this.letras.length - this.erros)) {
        this.etapa = 'ganhador'
      }
    },

    reset() {
      this.tela = 'inicio'
      this.etapa = 'palavra'
      this.palavra = ''
      this.dica = ''
      this.letras = []
      this.erros = 0
    }
  },
}
</script>

<style>
#app {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
