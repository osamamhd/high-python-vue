<template>
  <v-container>

    <h1 class="grey--text">Categories</h1>
    <v-layout row class="my-2">
      <CategoryCard 
        v-for="category in categories" 
        :key="category.id" 
        :category="category"/>
    </v-layout>

  </v-container>
</template>

<script>
import axios from 'axios'
import CategoryCard from '@/components/CategoryCard.vue'
export default {
    name: 'Categories',

    data() {
        return {
            categories: []
        }
    }, 

    components: {
        CategoryCard
    },

    mounted() {
        this.getCategories()
        document.title = 'Categories'
    }, 

    methods: {
        async getCategories() {
            await axios
                .get('/api/categories/')
                .then(response => {
                    this.categories = response.data
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