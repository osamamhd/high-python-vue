<template>
<div class="home">
  <v-container>

    <h1 class="grey--text text-uppercase">Articles</h1>
    <v-layout row class="my-2">
      <ArticleCard 
        v-for="article in articles" 
        :key="article.id" 
        :article="article"/>
    </v-layout>

  </v-container>
</div>

</template>

<script>
import axios from 'axios'
import ArticleCard from '@/components/ArticleCard.vue'
  export default {
    name: 'Home',

    data() {
      return {
        articles: []
      }
    }, 

    components: {
      ArticleCard,
    }, 

    mounted() {
      this.getArticles()
      document.title = 'High Python | Articles'
    }, 

    methods: {
      async getArticles() {
        await axios
          .get('/api/')
          .then(response => {
            this.articles = response.data
          })
          .catch(err => {
            console.log(err)
          })
      }
    }


  }
</script>
