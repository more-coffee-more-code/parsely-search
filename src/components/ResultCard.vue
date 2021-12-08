<template>
  <!-- <transition name="show"> -->
  <a :href="result.url" class="result-card__link" title="Read article">
    <div class="result-card">
      <figure class="result-card__thumbnail-wrapper">
        <img :src="result.image_url" alt="Thumbnail Image" class="result-card__thumbnail">
      </figure>
      <div class="result-card__content">
        <h3 class="result-card__headline">{{ formatTitle(result.title) }}</h3>
        <p class="result-card__author">{{ result.author }}</p>
        <p class="result-card__published-date">Published on {{ formatDate(result.pub_date) }}</p>
        <!-- <ul class="result-card__tags">
          <p class="result-card__label">Tags:</p>
          <li class="result-card__tag" v-for="tag in result.tags.slice(0, 2)" :key="tag">{{ formatTag(tag) }}</li>
        </ul> -->
      </div>
      <a :href="result.url" class="result-card__go-to" title="Go to article">Read &rarr;</a>
    </div>
  </a>
</template>
<script>
export default {
  name: 'ResultCard',
  props: {
    result: Object
  },
  data() {
    return {
      animate: true,
    }
  },
  methods: {
    formatDate(date) {
      let unformattedDate = new Date(date)

      let year = unformattedDate.getFullYear()
      let month = unformattedDate.toLocaleString('en-US', {month: 'long'})
      let day = unformattedDate.getDate()

      let formattedDate = `${month} ${day}, ${year}`
      return formattedDate
    },
    formatUrl(url) {
      return url.slice(0, 45) + '...'
    },
    formatTitle(title) {
      let isMobileDevice = window.innerWidth < 600
      if(isMobileDevice) {
        return title.slice(0, 25) + '...'
      }
      return title.slice(0, 50) + '...'
    },
    formatTag(tag) {
      let formattedTag = tag.split("-").map(a => a.charAt(0).toUpperCase() + a.substr(1)).join(", ")
      
      return formattedTag 
    },
  }
}
</script>
<style lang="scss" scoped>
@import '../assets/css/global-styles';

.result-card {
  width: 300px;
  max-height: 350px;
  margin: 30px;
  display: flex;
  flex-direction: column;
  box-shadow: $global-box-shadow;
  transition: all 0.3s cubic-bezier(.25,.8,.25,1);
  background-color: $black;
  color: $white;

  &:hover {
    box-shadow: $global-box-shadow-hover;
  }

  @include desktop {
    width: 600px;
    flex-direction: row;
  }
  
  &__link {
    text-decoration: none;

    &:focus {
      background: $gray-keyboard-tabbing;
    }
  }

  &__thumbnail-wrapper {
    width: 300px;
    height: 200px;

    & img {
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
  }

  &__content {
    padding: 10px;
    display: flex;
    flex-direction: column;
    text-align: left;

    @include desktop {
      width: 400px;
      padding: 10px 0 10px 20px;
    }
  }

  &__headline {
    color: $white;
    

    @include desktop {
      margin-top: 20px;
    }
  }

  &__author {
    padding: 10px 0 30px;
    color: $neon-green;
    font-size: $font-size-small;
  }

  &__published-date {
    font-size: $font-size-x-small;

    @include desktop {
      margin-top: 40px;
    }
  }

  &__go-to {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-decoration: none;
    background-color: $orange;
    color: $white;
    padding: 10px 0;
    font-weight: bold;
    cursor: pointer;

    &:hover {
      background-color: $orange-dark;
    }

    &:focus {
      color: $black;
      text-decoration: underline;
    }

    @include desktop {
      height: 200px;
      padding: 0 5px;
      width: 50px;
      align-content: center;
    }
  }

  &__label {
    font-size: $font-size-x-small;
  }

  &__tags {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    list-style: none;
    margin: 10px 0;
  }

  &__tag {
    font-size: $font-size-x-small;
  }
}
</style>