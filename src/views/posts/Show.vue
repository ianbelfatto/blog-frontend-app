<template>
  <div class="posts-show">
    <!-- <p>{{ post }}</p> -->
    <h2>{{ post.title }}</h2>
    <img :src="post.image" alt="" />
    <p>{{ post.body }}</p>
    <!-- <p>Posted by: {{ post.user.name }}</p> -->
    <router-link to="/posts" tag="button">Back to All Posts</router-link>
    |
    <router-link :to="`/posts/${post.id}/edit`" tag="button">Edit Post</router-link>
    |
    <button v-on:click="destroyPost()">Delete Post</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
    };
  },

  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Posts Object", response.data);
      this.post = response.data;
    });
  },

  methods: {
    destroyPost: function () {
      if (confirm("Are you sure?\nClick OK to delete!")) {
        axios.delete(`/posts/${this.post.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        });
      }
    },
  },
};
</script>
