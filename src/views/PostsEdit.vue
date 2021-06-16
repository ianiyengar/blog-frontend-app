<template>
  <div class="signup">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Body:</label>

        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>Image:</label>

        <input type="text" v-model="editPostParams.directions" />
      </div>
      <div>
        <label>UserID:</label>

        <input type="text" v-model="editPostParams.ingredients" />
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
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        console.log("show posts", response.data);

        this.editRecipeParams = response.data;
      });
    },
    updateRecipe: function () {
      axios

        .patch("/posts/" + this.$route.params.id, this.editRecipeParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
