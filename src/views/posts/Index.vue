<template>
  <div class="posts-index">
    <input v-model="searchTerm" type="text" list="titles" />
    <br />

    <datalist id="titles">
      <option v-for="post in posts" v-bind:key="post.id">
        {{ post.title }}
      </option>
    </datalist>

    <span v-if="filterBy(posts, searchTerm, 'title').length == 0">
      <p>No Results Found</p>
    </span>

    <button v-on:click="setSortAttribute('title')">Sort By Title</button>
    <button v-on:click="setSortAttribute('body')">Sort By Body</button>

    <div
      v-for="post in filterBy(
        orderBy(posts, sortAttribute),
        searchTerm,
        'title'
      )"
      v-bind:key="post.id"
    >
      <h2>{{ post.title }}</h2>
      <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" alt="" />
      </router-link>
      <p>{{ post.body }}</p>
      <p>{{ relativeDate(post.created_at) }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      searchTerm: "",
      sortAttribute: "title",
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log("Posts array", response.data);
      this.posts = response.data;
    });
  },

  methods: {
    relativeDate: function (dateIn) {
      return moment(dateIn).fromNow();
    },

    setSortAttribute: function (attribute) {
      this.sortAttribute = attribute;
    },
  },
};
</script>
