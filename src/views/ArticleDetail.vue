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
      <v-container v-show="!isLoading" class="mt-4 grey--text text--darken-4">
          <v-layout row>
            <v-flex xs12 md9>
                <v-card class="mx-md-2">
                   <v-img
                    class="white--text align-end"
                    height="150px"
                    :src="image"
                    /> 
                    <v-card-title class="d-flex justify-space-between">
                        <span class="text-uppercase">{{ title }}</span>
                        <span class="font-weight-light body-2">
                            <v-icon small class="pb-1">schedule</v-icon>
                            {{ created_at }}
                        </span>
                    </v-card-title>

                    <v-card-text class="text--primary pb-0">
                        <div>{{ description }}</div>
                    </v-card-text>

                    <v-card-subtitle class="pb-0 d-flex justify-space-between">
                        <span>
                            <v-icon small>local_offer</v-icon>
                            <span v-for="tag in tags" :key="tag">
                                {{ tag }},
                            </span>
                        </span>
                        <span>
                            <v-icon small class="pb-1">hourglass_bottom</v-icon>
                            {{ timeToRead }} min read
                        </span>
                    
                    </v-card-subtitle>

                    <VueShowdown class="mx-4 my-2 grey--text text--darken-3"
                    :markdown= "content"
                    />

                    <v-card-actions class="d-flex justify-space-between pb-4">
                        <span>
                        <v-btn
                            color="teal"
                            text small
                            @click="postHeart"
                        >
                        <v-icon>favorite</v-icon>
                            <span class="mx-1">{{ heart }}</span>
                            
                        </v-btn>

                        <v-btn
                            color="teal"
                            text small
                            @click="postLike"
                        >
                        <v-icon>thumb_up</v-icon>
                            <span class="mx-1 px-0">{{ like }}</span>
                        </v-btn>

                        <v-btn
                            color="teal"
                            text small
                            @click="postHappy"
                        >
                        <v-icon>emoji_emotions</v-icon>
                            <span class="mx-1">{{ happy }}</span>
                        </v-btn>
                        </span>

                        <span>
                        <v-btn
                            color="teal"
                            text small
                        >
                        <v-icon>account_circle</v-icon>
                            <span class="mx-1">{{ created_by }}</span>
                        </v-btn>
                        </span>
                    </v-card-actions>
                        
                </v-card>
            

                <div  v-for="comment in comments" :key="comment.id" class="mx-md-2 my-2 px-2 teal lighten-5  rounded">
                <v-list-item-content >
                        <v-list-item-title class="d-flex justify-space-between">
                            <span>
                                <v-icon>account_circle</v-icon> {{ comment.author }}
                            </span>
                            <span class="font-weight-light body-2">
                                <v-icon small class="pb-1">schedule</v-icon>
                                {{ comment.creation_date }}
                            </span>
                        </v-list-item-title>

                        <v-list-item-subtitle class="ml-5 ">
                            <div class="text-wrap caption">
                                <v-icon small>mode_comment</v-icon> {{ comment.text }}
                            </div>
                        
                        </v-list-item-subtitle>
                </v-list-item-content>
                </div>


                <v-form v-model="valid" id="commentForm">
                    <v-container>
                    <v-row>
                        <v-col
                        cols="12"
                        md="4"
                        >
                        <v-text-field
                            v-model="author"
                            :rules="authorRules"
                            :counter="50"
                            label="Author"
                            required
                        ></v-text-field>
                        </v-col>

                        <v-col
                        cols="12"
                        md="6"
                        >
                        <v-text-field
                            v-model="text"
                            :rules="textRules"
                            :counter="400"
                            label="Comment"
                            required
                        ></v-text-field>
                        </v-col>

                        <v-col
                        class="mt-md-4"
                        cols="12"
                        md="2"
                        >
                        <v-btn @click="postComment">
                            Submit
                        </v-btn>
                        </v-col>
                    
                    </v-row>
                    </v-container>
                </v-form>
            </v-flex>

            <v-flex lg3>
              <LatestArticles/>
            </v-flex>
          </v-layout>
          
        
      </v-container>
      
  </div>
</template>

<script>
import axios from 'axios'
import { VueShowdown } from 'vue-showdown'
import LatestArticles from '@/components/LatestArticles'
export default {
    name: 'ArticleDetail',

    data() {
        return {
            artilce: [],
            title:'',
            description: '',
            content: '',
            category: '',
            image: '',
            tags: [],
            heart: '',
            like: '',
            happy: '',
            id: '',
            created_by: '',
            created_at: '',
            timeToRead: '',
            comments: [],
            isLoading: true,

            // comment form
            valid: false,
            author: '',
            text: '',
            authorRules: [
                v => !!v || 'Author is required',
                v => v.length <= 50 || 'Name must be less than 50 characters',
            ],
            textRules: [
                v => !!v || 'Text is required',
                v => v.length <= 400 || 'Text must be less than 400 characters',
            ],
        }
    },
    
    components: {
        VueShowdown,
        LatestArticles,
    },

    mounted() {
        this.getArticleDetail()
        
    },

    methods: {
        async getArticleDetail() {
            
            const category_slug = this.$route.params.category_slug
            const article_slug = this.$route.params.article_slug

            await axios
                .get(`/api/${category_slug}/${article_slug}/`)
                .then(response => {
                    this.artilce = response.data
                    document.title = 'Articles | ' + this.artilce.title
                    this.title = this.artilce.title
                    this.content = this.artilce.content
                    this.description = this.artilce.description
                    this.category = this.artilce.category
                    this.image = this.artilce.get_image
                    this.tags = this.artilce.tags
                    this.heart = this.artilce.heart
                    this.like = this.artilce.like
                    this.happy = this.artilce.happy
                    this.id = this.artilce.id
                    this.created_by = this.artilce.created_by
                    this.created_at = this.artilce.creation_date
                    this.timeToRead = Math.ceil(this.content.length/1500)
                    this.getComments()
                    this.isLoading = false
                })
                .catch(err => {
                    console.log(err)
                })
        },
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
        },

        async getComments() {
            await axios
                .get(`/api/${this.artilce.id}/comments/`)
                .then(response => {
                    this.comments = response.data
                })
                .catch(err => {
                    console.log(err)
                })
        }, 

        postComment() {
            const formData = {
                author: this.author,
                text: this.text
            }
            axios
                .post(`/api/${this.artilce.id}/comments/`, formData)
                .then(response => {
                    this.comments.push(response.data)
                    document.getElementById("commentForm").reset();
                    this.text = ' '
                })
                .catch(err => {
                    console.log(err)
                })
        }
    }
}
</script>
