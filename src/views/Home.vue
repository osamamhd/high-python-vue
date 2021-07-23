<template>
<div class="home">
  <v-container v-show="isLoading"  style="height: 400px;">
    <v-row
        class="fill-height"
        align-content="center"
        justify="center"
    >
        <v-col
        class="text-subtitle-1 text-center"
        cols="12"
        >
        Loading Content
        </v-col>
        <v-col cols="6">
        <v-progress-linear
            color="teal accent-4"
            indeterminate
            rounded
            height="6"
        ></v-progress-linear>
        </v-col>
    </v-row>
  </v-container>
  <v-container v-show="!isLoading">
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
        articles: [],
        isLoading: true,

      }
    }, 

    components: {
      ArticleCard,
    }, 

    mounted() {
      this.getArticles()
      document.title = 'HighPython | Articles'
    }, 

    methods: {
      async getArticles() {
        await axios
          .get('/api/')
          .then(response => {
            this.articles = response.data
            this.isLoading = false
          })
          .catch(err => {
            console.log(err)
          })
      }
    }


  }
</script>
