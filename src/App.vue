<template>
  <div id="app">
    <div id="nav">
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <router-link class="navbar-brand" to="/"> Home </router-link>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <router-link class="nav-link" to="/posts"> Posts </router-link>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" to="/posts/new">
                  New Post
                </router-link>
              </li>
            </ul>
            <form class="d-flex">
              <input
                class="form-control me-2"
                type="search"
                placeholder="Search"
                aria-label="Search"
              />
              <button class="btn btn-outline-success" type="submit">
                Search
              </button>
            </form>
          </div>
        </div>
      </nav>
      <router-link to="/"> Home </router-link> |
      <router-link to="/posts"> Posts </router-link> |
      <router-link to="/posts/new"> New Post </router-link> |
      <span v-if="!isLoggedIn()">
        <router-link to="/signup"> Signup </router-link> |
        <router-link to="/login"> Login </router-link>
      </span>
      <span v-if="isLoggedIn()">
        <router-link to="/logout"> Logout </router-link>
      </span>
    </div>
    <div id="temporary">{{ flashMessage }}</div>
    <router-view />
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      flashMessage: "Testme",
    };
  },

  created: function () {},

  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
