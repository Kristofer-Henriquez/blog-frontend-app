<template>
  <div class="show">
    <h1>{{ message }}</h1>
    <h2> {{post.title}} </h2>
    <h3> {{post.image}} </h3>
    <p> {{post.body}} </p>

    <img v-bind:src="post.image">
    <br>
    <a v-bind:href="`/posts/${post.id}/edit`"> Edit this post! </a>

    <p><button v-on:click="destroyPost()"> Delete this post </button></p>

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
    },
    destroyPost: function() {
      console.log("deleting this post...");

      axios.delete(`/api/posts/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.$router.push("/posts")
      })
    }
  }
};
</script>