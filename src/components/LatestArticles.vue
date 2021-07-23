<template>
<div>
    <v-layout column>
        <span class="ml-3 mt-md-0 mt-4 font-weight-medium grey--text text--darken-3">
            Latest Articles
        </span>

          <ArticleCard 
          v-for="article in articles" 
          :key="article.id" 
          :article="article"/>
      
    </v-layout>
</div>
</template>

<script>
import ArticleCard from '@/components/ArticleCard'
import axios from 'axios'

export default {
    name: 'LatestArticles',

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
    }, 

    methods: {
      async getArticles() {
        await axios
          .get('/api/latest-articles')
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

<style>

</style>