<template>
  <v-flex xs12 sm6 lg3>
    <v-card
        class="mx-2 my-2"
        max-width="400"
    >
        <v-img
        class="white--text align-end"
        height="150px"
        :src="category.get_cover"
        >
        <v-card-title>{{ category.title }}</v-card-title>
        </v-img>

        <v-card-text class="text--primary pb-0">
        <div>{{ category.description }}</div>
        </v-card-text>

        <v-card-subtitle class="pb-0">
        
        </v-card-subtitle>

        <v-card-actions>
        

        <v-btn
            class="px-1"
            color="teal"
            text small
        >
        <v-icon>article</v-icon>
            <span class="mx-1">{{ category.articles_count }} Articles</span>
        </v-btn>

        <v-btn
            class="px-1"
            color="teal"
            text small 
            router :to="category.get_absolute_url"
        >
        <v-icon>visibility</v-icon>
            <span class="mx-1">View All</span>
        </v-btn>
        </v-card-actions>
    </v-card>
</v-flex>
</template>

<script>
export default {
    name: 'CategoryCard',

    props: {
        category: Object
    }
}
</script>

<style>

</style>