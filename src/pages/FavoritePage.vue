<template>
  <div class="container">
    <h1 class="title">Favorite recipe:</h1>
    <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this page</router-link>
    <div v-if="flagResponse">
      <SearchResults title="Results" :results="results"></SearchResults>
    </div>


  </div>
</template>

<script>
import SearchResults from "../components/SearchResults";
export default {
  name: "Search",
  data() {
    return {
      results:[],
      flagResponse: false
    };
  },
  async created(){
    if (this.$root.store.username) {
        try {
            const response = await this.axios.get(this.$root.store.server_domain + "/users/favorites", { withCredentials: true});
            this.results = response.data
            this.flagResponse = true
        }
        catch (err) {
            console.log("error.response.status", error.response.status);
        }
    }

  },
  components: { SearchResults }
};
</script>


<style lang="scss" scoped>
.container {
  max-width: 400px;
}
</style>
