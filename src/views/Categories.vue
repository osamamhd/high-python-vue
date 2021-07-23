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
    <h1 class="grey--text text-uppercase">Categories</h1>
    <v-layout row class="my-2">
      <CategoryCard 
        v-for="category in categories" 
        :key="category.id" 
        :category="category"/>
    </v-layout>
  </v-container>
</div>
</template>

<script>
import axios from 'axios'
import CategoryCard from '@/components/CategoryCard.vue'
export default {
    name: 'Categories',

    data() {
        return {
            categories: [],
            isLoading: true,
        }
    }, 

    components: {
        CategoryCard
    },

    mounted() {
        this.getCategories()
        document.title = 'HighPython | Categories'
    }, 

    methods: {
        async getCategories() {
            await axios
                .get('/api/categories/')
                .then(response => {
                    this.categories = response.data
                    this.isLoading = false
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