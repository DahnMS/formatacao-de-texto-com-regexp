<template lang="pug">
    #app
        Editor(texto="", textoFormatado="")
</template>

<script>
import Editor from './components/Editor.vue';

export default {
  name: 'app',
  components: {
    Editor
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>