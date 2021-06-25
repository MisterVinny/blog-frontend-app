<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>New Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <img v-if="status" :src="`https://http.cat/${status}`" alt="" />
      <div class="form-group">
        <label>Title: </label>
        <input type="text" class="form-control" v-model="newPostParams.title" />
      </div>

      <div class="form-group">
        <label>Body: </label>
        <input
          v-if="
            newPostParams.body.length <= 20 && newPostParams.body.length >= 5
          "
          type="text"
          class="form-control"
          v-model="newPostParams.body"
        />
        <input
          v-else
          type="text"
          class="danger-box"
          v-model="newPostParams.body"
        />
        <br />
        <small v-if="newPostParams.body.length < 5">
          Body must be greater than 5 characters.</small
        >
        <small>{{ 20 - newPostParams.body.length }} characters remaining</small>
      </div>

      <div class="form-group">
        <label>Image: </label>
        <input type="text" class="form-control" v-model="newPostParams.image" />
      </div>

      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<style>
.danger-box {
  background-color: red;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPostParams: {
        body: "",
      },
      errors: [],
      status: "",
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
          this.status = error.response.status;
        });
    },
  },
};
</script>
