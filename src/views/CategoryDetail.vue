<template>
<div>
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
            isLoading: true,
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
                    document.title = 'Categories | ' + this.category.title
                    this.isLoading = false
                })
                .catch(err => {
                    console.log(err)
                })
        }
    }
}
</script>
