<template>
  <div class="signup">
    <img v-if="status" v-bind:src="`https://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="submit()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <label>Imgae:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <div>
        <label>User:</label>
        <input type="text" v-model="newPostParams.user" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
      status: null,
    };
  },
  methods: {
    submit: function () {
      console.log("THESE ARE MY PARAMS", this.newPostParams);
      axios
        .post("/posts", this.newRecipeParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>
