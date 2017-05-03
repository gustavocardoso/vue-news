<template>
  <div class="newslist">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img v-bind:src="article.urlToImage" class="media-object">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{ article.title }}</a>
            </h4>
            <h5>by {{ article.author }}</h5>
            <p>{{ article.description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'newslist',
    props: ['source'],

    data() {
      return {
        articles: []
      }
    },

    methods: {
      updateSource: function(value) {
        this.$http.get('https://newsapi.org/v1/articles?source=' + value + '&apikey=1c9f77e6f18c4eb9b146aa2c8b6cfc40')
          .then(response => {
            this.articles = response.data.articles
          })
      }
    },

    watch: {
      source: function(value) {
        this.updateSource(value)
      }
    }
  }
</script>

<style scoped>
  .media {
    text-align: left;
    border-top: 1px solid lightgrey;
    padding-top: 20px;
  }
  .media-object {
    width: 128px;
    padding: 10px;
  }
</style>