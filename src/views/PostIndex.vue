<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2> See below posts! </h2>

    <input type="text" v-model="searchentry" list="titles">

    <datalist id="titles">
      <option v-for="post in orderBy(posts, 'title')"> {{ post.title}} </option> 
    </datalist>

    <div v-for="post in filterBy(posts, searchentry, 'title')">
      <h3><a v-bind:href="`/posts/${post.id}`">{{ post.title }}</a></h3>
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
import Vue2Filters from "vue2-filters";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      posts: [],
      searchentry: ""
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
  },
  mixins: [Vue2Filters.mixin],
};
</script>