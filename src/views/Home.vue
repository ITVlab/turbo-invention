<template>
  <div class="home">
    <NewsFeed></NewsFeed>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import NewsFeed from "@/components/NewsFeed.vue";

export default {
  name: "home",
  components: {
    HelloWorld,
    NewsFeed
  }
};
</script>
