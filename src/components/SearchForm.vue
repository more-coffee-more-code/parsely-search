<template>
  <form class="search-form" @submit.prevent="search">
    <label for="search" class="search-form__label">Search Ars Technica...</label>
    <div class="search-form__search-wrapper">
      <input type="search" name="search" id="" class="search-form__input" v-model="userQuery">
      <div class="search-form__button-wrapper">
        <button type="submit" class="search-form__button" @click="search">Search</button>
      </div>
    </div>
    <ul class="search-form__results">
      <results-card v-for="result in results" :key="result" :result="result"/>
    </ul>
  </form>
  <button type="submit" class="search-form__pagination" v-show="this.showLoadMore === true" @click.prevent="next(this.userQuery)">Load More &rarr;</button>
</template>
<script>
import ResultsCard from './ResultCard.vue'

export default {
  name: 'SearchForm',
  components: {
    ResultsCard
  },
  data() {
    return {
      userQuery: '',
      results: Object,
      pageCount: 1,
      showLoadMore: false
    }
  },
  methods: {
    getSearchUrl(query) {
      let string = require("string-sanitizer")
      this.userQuery = string.sanitize(query)
      return `https://api.parsely.com/v2/search?apikey=arstechnica.com&q=${this.userQuery}&days=30` 
    },
    search(url) {
      url = this.getSearchUrl(this.userQuery)
      fetch(url)
      .then(response => response.json())
      .then(data => this.results = data.data)

      this.showLoadMore = true
    },
    next(query) {
      // attempted to create pagination. clean up required
      let newUrl = `https://api.parsely.com/v2/search?apikey=arstechnica.com&q=${query}&days=70&page=${this.pageCount += 1}`

      fetch(newUrl)
      .then(response => response.json())
      .then(data => this.results = data.data);
      return this.search(newUrl)
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../assets/css/global-styles';

.search-form {
  &__search-wrapper {
    width: 90%;
    display: flex;
    flex-direction: row;
    margin: 15px auto 50px;

    @include desktop {
    max-width: 700px;
    }
  }

  &__label {
    color: $orange-dark;
    font-weight: bold;
    font-size: $font-size-large;
  }

  &__input {
    width: 100%;
    height: 50px;
    padding: 10px 20px;
    border: solid 1px $orange;
    color: $orange-dark;
    font-weight: bold;
    font-size: $font-size-large;
  }

  &__button {
    &-wrapper {
      text-align: center;
      overflow: hidden;
      max-height: 50px;
      max-width: 120px;
      width: 100%;

      @include desktop {
        max-width: 150px;
      }
    }

    background: none;
    border: none;
    background-color: $orange;
    width: 100%;
    height: 100%;
    padding: 10px 20px;
    cursor: pointer;
    font-size: $font-size-large;
    color: $white;
    margin-left: -1px;
    transition: transform .2s;
    display: flex;
    flex-direction: row;
    justify-content: center;
    
    &:hover {
     transform: scale(1.2);
     background-color: $orange-dark;
    }
  }

  &__results {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }

  &__pagination {
    background-color: $white;
    color: $orange-dark;
    padding: 10px 20px;
    border: none;
    font-size: $font-size-x-large;
    cursor: pointer;

    &:hover {
      text-decoration: underline;
    }

    &:focus {
      background: $gray-keyboard-tabbing;
    }
  }
}
</style>