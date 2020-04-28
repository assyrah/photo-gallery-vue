<template>
  <div class="container">
    <h1 class="title">{{title}}</h1>
    <div class="gallery">
        <ul class="categories">
          <li  
            v-for="category in categories" 
            class="category" 
            :key="category" 
            @click="selectCategory(category)"
            :class="{active : category == activeCategory}"
          >
              {{category}}
          </li>
        </ul>
      <div class="photos"> 
        <p v-if="!photos.length">Select category from the left to see images here.</p>
        <app-card
          v-for="(photo, index) in photos"
          :photo="photo"
          :key="index">
        </app-card>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
import appCard from './Card'
export default {
  name: 'gallery',
  components: {
    'app-card': appCard,
  },
  data: () => ({
    photos: [],
    title: 'Gallery Categories',
    categories: ['flower', 'sunset', 'farm', 'fruit', 'insect', 'cat', 'dog', 'bird'],
    activeCategory: ''
  }),
  methods: {
    selectCategory: function (category) {
      this.title = category + ' Photo Gallery'
      this.activeCategory = category
      $.ajax({
        url: `https://api.flickr.com/services/feeds/photos_public.gne?tags=${category}&format=json&jsoncallback=?`,
        dataType: 'json'
      }).then((data) => {
        this.photos = data.items
      })
    }
  }
}
</script>

<style scoped lang="scss">
  .gallery {
    text-align: left;
    display: flex;
    flex-direction: column;
    @media (min-width: $breakpoint-lg) {
      flex-direction: row;
    }
  }

  .categories {
    list-style: none;
    text-transform: capitalize;
    padding: 0;
    width: 100%;
    flex: 1;
    font-weight: bold;
    font-size: $font-size-sm;
    text-align: center;
    @media (min-width: $breakpoint-lg) {
      width: 150px;
      font-size: $font-size-base;
      text-align: left;
    }
  }

  .category {
    cursor: pointer;
    display: inline;
    padding: .15rem;
    &.active {
      color: $color-font-primary-light;
    }
    &:hover {
      color: $color-font-primary;
    }
    @media (min-width: $breakpoint-lg) {
      padding: 0;
      padding-bottom: 1rem;
      display: block;
    }
  }

  .photos {
    display: flex;
    flex-wrap: wrap;
    flex: 6;
  }

  .title {
    text-transform: capitalize;
    text-align: center;
  }
</style>
