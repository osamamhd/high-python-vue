<template>
<div class="home">
  <v-container>
    <h1 class="grey--text text-uppercase">{{category.title}}</h1>
      
    <v-layout row class="my-2">
      <ArticleCard 
        v-for="article in category.articles" 
        :key="article.id" 
        :article="article"/>
    </v-layout>

  </v-container>
</div>
  
</template>

<script>
import ArticleCard from '@/components/ArticleCard.vue'
import axios from 'axios'
export default {
    name: 'CategoryDetail', 

    components: {
        ArticleCard
    }, 

    data() {
        return {
            category: [],
        }
    }, 

    mounted() {
        this.getCategory()
    }, 

    methods: {
        getCategory() {
            const category_slug = this.$route.params.category_slug
            axios
                .get(`/api/${category_slug}/`)
                .then(response => {
                    this.category = response.data
                    document.title = this.category.title
                })
                .catch(err => {
                    console.log(err)
                })
        }
    }
}
</script>
