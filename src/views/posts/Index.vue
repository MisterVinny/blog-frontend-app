<template>
  <div class="posts-index">
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.title }}</h2>
      <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" alt="" />
      </router-link>
      <p>{{ post.body }}</p>
      <!-- <router-link to="/posts/1"></router-link> behaves like an a tag but has no page refresh that the a tag suffers from. Interpreted into a custom a-tag under the hood. Wrap around the thing you want to click on.-->
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log("Posts array", response.data);
      this.posts = response.data;
    });
  },
};
</script>
