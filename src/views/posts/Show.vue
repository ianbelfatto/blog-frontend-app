<template>
  <div class="posts-show">
    <!-- <p>{{ post }}</p> -->
    <h2>{{ post.title }}</h2>
    <img :src="post.image" alt="" />
    <p>{{ post.body }}</p>
    <!-- <p>Posted by: {{ post.user.name }}</p> -->
    <router-link to="/posts">Back to All Posts</router-link>
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
};
</script>
