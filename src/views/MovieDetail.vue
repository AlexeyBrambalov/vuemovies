<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>{{ movie.Plot }}</p>
    <router-link to="/" tag="button" class="back-button">
      Back
    </router-link>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${process.env.VUE_APP_APIKEY}&i=${route.params.id}&plot=full`
      )
        .then((res) => res.json())
        .then((data) => {
          movie.value = data;
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style lang="scss">
.movie-detail {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
  .back-button {
    width: 100%;
    text-align: center;
    max-width: 100px;
    background-color: #42b883;
    padding: 5px;
    border-radius: 8px;
    color: #fff;
    font-size: 15px;
    text-transform: uppercase;
    transition: 0.4s;
    &:active {
      background-color: #3b8070;
    }
  }
  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
    margin-top: 16px;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
    margin-bottom: 20px;
  }
}
</style>
