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
        <label>Title: </label>
        <input
          type="text"
          class="form-control"
          v-model="editPostParams.title"
        />
      </div>

      <div class="form-group">
        <label>Body: </label>
        <input type="text" class="form-control" v-model="editPostParams.body" />
      </div>

      <div class="form-group">
        <label>Image: </label>
        <input
          type="text"
          class="form-control"
          v-model="editPostParams.image"
        />
      </div>

      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
    <hr />
    <div>
      <button v-on:click="deletePost()">Delete Post</button>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "EditPost",
      editPostParams: {},
      errors: [],
    };
  },

  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post object", response.data);
      this.editPostParams = response.data;
    });
  },

  methods: {
    editPost: function () {
      axios
        .patch(`/posts/${this.$route.params.id}`, this.editPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/posts/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(error.response.data.message);
        });
    },
    deletePost: function () {
      if (confirm("Do you really want to delete this post?")) {
        axios.delete(`/posts/${this.editPostParams.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        });
      }
    },
  },
};
</script>
