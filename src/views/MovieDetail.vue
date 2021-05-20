<template>
  <div class="movie-detail">
    <h2>{{movie.Title}}</h2>
    <p>{{ movie.Year }}</p>
    
    <div class="column">
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    </div>
    <div class="column">
        <p>{{ movie.Plot }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
export default {
  setup () {
    const movie = ref({});
    const route = useRoute();
    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data;
        });
    });
    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;
  h2 {
    color: #FFF;
    font-size: 38px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 500px;
    margin-bottom: 16px;
  }
  p {
    color: #FFF;
    font-size: 20px;
    line-height: 1.6;
  }
}
</style>

