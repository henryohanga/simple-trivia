<template>
  <div class="home">
    <div v-if="loading" class="loading">Loading...</div>
    <div v-if="error" class="error">{{ error }}</div>
    <Categories :categories="categories"></Categories>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import Categories from "@/components/Categories";
import axios from "axios";

export default {
  name: "home",
  components: {
    // HelloWorld,
    Categories
  },
  data() {
    return {
      loading: false,
      categories: [],
      error: null
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      this.error = null;
      this.categories = [];
      this.loading = true;

      axios
        .get("https://opentdb.com/api_category.php")
        .then(response => {
          this.categories = response.data.trivia_categories;
          this.loading = false;
        })
        .catch(err => {
          this.loading = false;
          this.error = err;
        });
    }
  }
};
</script>
