<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>New Post</h1>
      <ul>
        <li class="text-errors" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>

      <div class="form-group">
        <label>Title: </label>
        <input type="text" class="form-control" v-model="newPostParams.title" />
      </div>

      <div class="form-group">
        <label>Body: </label>
        <input type="text" class="form-control" v-model="newPostParams.body" />
      </div>

      <div class="form-group">
        <label>Image: </label>
        <input type="text" class="form-control" v-model="newPostParams.image" />
      </div>

      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "NewPost",
      newPostParams: {},
      errors: [],
    };
  },

  created: function () {},

  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(error.response.data.message);
        });
    },
  },
};
</script>
