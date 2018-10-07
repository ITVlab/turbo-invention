<template>
<v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-img
          class="white--text"
          height="200px"
          :src="currentPost.better_featured_image.source_url"
        >
          <v-container fill-height fluid>
            <v-layout fill-height>
              <v-flex xs12 align-end flexbox>
                <span class="headline" v-html="currentPost.title.rendered"></span>
              </v-flex>
            </v-layout>
          </v-container>
        </v-img>
        <v-card-title>
          <div class="text-xs-center">
            <span class="grey--text">Grey</span><br>
            <span>Whitehaven Beach</span><br>
            <span>Whitsunday Island, Whitsunday Islands</span>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn flat color="orange">Share</v-btn>
          <v-btn flat color="orange">Explore</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>   
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
  props: ["currentPost"],
  // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get(
        `http://data.androidtv.news/wp-json/wp/v2/posts/${this.currentPost}`
      );
      this.posts = response.data;
    } catch (e) {
      this.errors.push(e);
    }
  }
};
</script>
<style lang="scss" scoped>
</style>
