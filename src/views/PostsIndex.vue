<template>
  <div>
    <h1>All posts</h1>
    <div>
      Search by title:
      <input type="text" v-model="searchFilter" list="post-titles" />
      <datalist id="post-titles">
        <option v-for="post in posts" v-bind:key="post.id">{{ post.title }}</option>
      </datalist>
    </div>
    <div
      class="row"
      is="transition-group"
      appear
      enter-active-class="animated zoomInDown"
      leave-active-class="animated fadeOutLong"
    >
      <div class="col-sm-4" v-for="post in filterBy(posts, searchFilter, 'title')" v-bind:key="post.id">
        <div class="card">
          <img v-bind:src="post.image_url" class="card-img-top" alt="..." />
          <div class="card-body">
            <h2 class="card-title">{{ post.title }}</h2>
            <p class="card-text">by {{ post.chef }}</p>
            <a v-bind:href="`/posts/${post.id}`" class="btn btn-primary">More info</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.card img {
  object-fit: cover;
  height: 300px;
}
.fadeOutLong {
  opacity: 0;
  transition: opacity 5s ease;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      searchFilter: "",
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        console.log("index posts", response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
// title // body // image // user_id
