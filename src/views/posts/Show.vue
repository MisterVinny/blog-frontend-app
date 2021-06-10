<template>
  <div class="posts-show">
    <div>
      <router-link to="/posts/">
        <img :src="post.image" alt="" />
      </router-link>
      <h1>{{ post.title }}</h1>
      <p>{{ post.body }}</p>
    </div>
    <div>
      <router-link :to="`/posts/${post.id}/edit`">Edit Post</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "hello?",
      post: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post object:", response.data);
      this.post = response.data;
    });
  },
};
</script>
