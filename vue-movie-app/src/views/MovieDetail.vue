<template>
  <div class="movie-detail">
    <h2>{{movie.Title}}</h2>
    <p>Year: {{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>Sinopse:</p> <br>
    <p>{{ movie.Plot }}</p>
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
      fetch(`http://www.omdbapi.com/?apiKey=${env.apiKey}&i=${route.params.id}&plot=full`)
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
  align-items: center;
  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 5px;
    text-align: center;
  }
  img {
    align-items: center;
  }
  .featured-img {
    display: block;
    max-width: 100%;
    margin-left: 20px;
    margin-bottom: 16px;
    align-items: center;    
  }
  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
    text-align: justify;
    margin-right: 5px;
  }
}
</style>