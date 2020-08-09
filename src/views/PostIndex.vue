<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2> See below posts! </h2>
    <div v-for="post in posts">
      {{post.title}}
      {{post.image}}
      <hr>
      <br>
      <img v-bind:src="post.image">
    </div>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      posts: []
    };
  },
  created: function() {
    this.IndexPosts();
  },
  methods: {
    IndexPosts: function() {
      console.log("this is posts index...")
      axios.get("/api/posts").then(response => {
        console.log(response.data);
        this.posts = response.data;
      });
    }
  }
};
</script>