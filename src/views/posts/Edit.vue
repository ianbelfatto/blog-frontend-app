<template>
  <div class="posts-edit">
    <form v-on:submit.prevent="editPost()">
      <h1>Edit Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="editPostParams.title" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="editPostParams.body" />
      </div>
      <div class="form-group">
        <label>Image URl:</label>
        <input type="text" class="form-control" v-model="editPostParams.image" />
      </div>
      <br />
      <router-link :to="`/posts/${editPostParams.id}`" tag="button">Back to Current Post</router-link>
      |
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
    <br />
    editPostParams: {{ editPostParams }}
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Posts Object", response.data);
      this.editPostParams = response.data;
    });
  },
  methods: {
    editPost: function () {
      axios
        .patch(`/posts/${this.editPostParams.id}`, this.editPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/posts/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
