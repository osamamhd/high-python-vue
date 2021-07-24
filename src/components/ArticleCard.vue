<template>

<v-flex xs12 sm6 lg3>
    <v-card
        class="mx-2 my-2"
        max-width="400"
    >
        <v-img
        class="white--text align-end"
        height="100px"
        :src="article.get_thumbnail"
        >
        <v-card-title class="pb-0">{{ article.title }}</v-card-title>
        </v-img>

        <v-card-text class="text--primary pb-0">
        <div>{{ article.description }}</div>
   
        </v-card-text>

        <v-card-subtitle class="pb-0">
        <v-icon small>local_offer</v-icon>
        <span v-for="tag in article.tags" :key="tag">
            {{ tag }},
        </span>
        </v-card-subtitle>

        <v-card-actions>
        <v-btn
            class="px-1"
            color="teal"
            text small
            @click="postHeart"
        >
        <v-icon>favorite</v-icon>
            <span class="mx-1">{{ heart }}</span>
            
        </v-btn>

        <v-btn
            class="px-1"
            color="teal"
            text small
            @click="postLike"
        >
        <v-icon>thumb_up</v-icon>
            <span class="mx-1 px-0">{{ like }}</span>
        </v-btn>

        <v-btn
            class="px-1"
            color="teal"
            text small
            @click="postHappy"
        >
        <v-icon>emoji_emotions</v-icon>
            <span class="mx-1">{{ happy }}</span>
        </v-btn>

        <v-btn
            class="px-1"
            color="teal"
            text small 
            router :to="article.get_absolute_url"
        >
            Read Now
            
        </v-btn>
        </v-card-actions>
    </v-card>
</v-flex>
</template>

<script>
import axios from 'axios'
export default {
    name: 'ArticleCard',

    props: {
        article: Object
    }, 

    data() {
        return {
            heart: this.article.heart,
            like: this.article.like,
            happy: this.article.happy,
            id: this.article.id
        }
    }, 

    methods: {
       
        postHeart() {
            axios
                .post(`/api/${this.id}/heart/`, this.heart)
                .then(this.heart++)
                .catch(err => {
                    console.log(err)
                })
        },

        postLike() {
            axios
                .post(`/api/${this.id}/like/`, this.like)
                .then(this.like++)
                .catch(err => {
                    console.log(err)
                })
        },

        postHappy() {
            axios
                .post(`/api/${this.id}/happy/`, this.happy)
                .then(this.happy++)
                .catch(err => {
                    console.log(err)
                })
        }
    }

}
</script>
