<template>
  <div id="app">
    <nav class="navbar navbar-light bg-light">
      <a class="navbar-brand">Navbar</a>
      <form class="form-inline">
        <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
      </form>
    </nav>
    <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/about">About</router-link>
      |
      <router-link to="/signup">Signup</router-link>
      |
      <router-link to="/login">Login</router-link>
      |
      <router-link to="/logout">Logout</router-link>
      |
      <router-link to="/postsindex">All Posts</router-link>
      |
      <router-link to="/posts/new">New Post</router-link>
      |
      <router-link to="/posts/1">Posts Show</router-link>
      |
      <router-link to="/posts/:id/edit">Posts Edit</router-link>
    </div>
    <div class="container">
      <div v-if="flashMessage" class="alert alert-success" role="alert">{{ flashMessage }}</div>
      <router-view />
    </div>
  </div>
</template>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
<script>
export default {
  data: function () {
    return {
      flashMessage: null,
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
