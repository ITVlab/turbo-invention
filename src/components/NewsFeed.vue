<template>
  <div>
      <v-container grid-list-md text-xs-center>
      <v-layout row wrap>
    <v-flex xs12 sm4  v-for="post of posts" :key="post.id">
      <v-card>
        <v-img
          :src="post.better_featured_image.source_url"
          aspect-ratio="2"
        ></v-img>

        <v-card-title primary-title>
            <h3 class="headline mb-0" v-html="post.title.rendered"></h3>
          <div class="text-truncate ">
            <div class="body-1" v-html="post.excerpt.rendered"></div>
          </div>
        </v-card-title>

        <v-card-actions>
            <router-link :to="{ name: 'post', params: { id: post.id, currentPost: post }}"><v-btn flat color="black">Share</v-btn></router-link>
            <router-link :to="{ name: 'post', params: { id: post.id, currentPost: post }}"><v-btn flat color="black">Read More</v-btn></router-link>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
      </v-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      posts: [],
      errors: []
    };
  },
  // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get(
        `https://api.androidtv.news/wp-json/wp/v2/posts`
      );
      this.posts = response.data;
    } catch (e) {
      this.errors.push(e);
    }
  }
};
</script>
