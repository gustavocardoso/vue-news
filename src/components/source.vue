<template>
  <div class="sourceselection">
    <div class="jumbotron">
      <h4><span class="glyphicon glyphicon-list-alt icon"></span>Select news source</h4>
      <select class="form-control" v-on:change="sourceChanged">
        <option v-bind:value="source.id" v-for="source in sources">{{ source.name }}</option>
      </select>

      <div v-if="source">
        <h6>{{ source.description }}</h6>
        <a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go to {{ source.name }} website</a>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'sourceselection',

    data() {
      return {
        sources: [],
        source: ''
      }
    },

    created: function() {
      this.$http.get('https://newsapi.org/v1/sources?language=en')
        .then(response => {
          this.sources = response.data.sources
          this.sources.unshift({id: 0, name: 'select a source'})
        })
    },

    methods: {
      sourceChanged: function(e) {
        if (e.target.value !== '0') {
          this.sources.map((source) => {
            if (source.id === e.target.value) {
              this.source = source
            }
          })

          this.$emit('sourceChanged', e.target.value)
        }
      }
    }
  }
</script>

<style scoped>
  .icon {
    margin-right: 10px;
  }
</style>