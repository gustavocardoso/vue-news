<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <h1>{{ title }}</h1>

    <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>
    <NewsList v-bind:source="source"></NewsList>
  </div>
</template>

<script>
  import SourceSelection from './components/source'
  import NewsList from './components/list'

  export default {
    name: 'app',
    
    components: {
      SourceSelection,
      NewsList
    },

    data() {
      return {
        title: 'Vue News',
        source: ''
      }
    },

    methods: {
      sourceChanged: function(source) {
        this.source = source
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
  width: 100px;
}
</style>
