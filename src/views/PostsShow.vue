<template>
  <div class="show">
    <h1>{{ message }}</h1>
    <h2> {{post.title}} </h2>
    <h3> {{post.image}} </h3>
    <p> {{post.body}} </p>

    <img v-bind:src="post.image">
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "This is the show page!",
      post: {}
    };
  },
  created: function() {
    this.showPost();
  },
  methods: {
    showPost: function() {
      console.log("individual post");

      axios.get("/api/posts/" + this.$route.params.id).then(response => {
        console.log(response);
        this.post = response.data;
      });
    }
  }
};
</script>