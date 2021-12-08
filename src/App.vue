<template>
<div>
  <search-form /> 
</div>
</template>
<script>
import SearchForm from './components/SearchForm.vue'

export default {
  name: 'App',
  components: {
    SearchForm
  }
}
</script>

<style lang="scss">
@import './assets/css/global-styles';

* {
  margin: 0;
  padding: 0;
}

input:focus {
  background: $lightgray-search-background;
  transition: .5s all;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 100px;
  padding-bottom: 30px;
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
}
</style>
