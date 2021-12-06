<template>
  <div class="search-form">
    <input type="search" name="" id="" v-model="userQuery">
    <button type="submit" @click="search">Search</button>
  </div>
</template>
<script>
export default {
  name: 'SearchForm',
  data() {
    return {
      userQuery: String
    }
  },
  mounted() {
    this.getSearchUrl()
  },
  methods: {
    getSearchUrl(query = 'apple', days=30) {
      return `https://api.parsely.com/v2/search?apikey=arstechnica.com&q=${query}&days=${days}` 
    },
    search(days = 30) {
      let url = getSearch(this.userQuery, days)
      
      fetch(url)
      .then(response => response.json())
      .then(data => console.log(data));
    }
  }
}
</script>
<style lang="scss" scoped>
.search-form {

}
</style>