<template>
  <div class="movie-page">
    <div class="movie-filter q-ml-md q-mr-xl">
      <MovieFilter @parametersChange="actualizarFiltros" />
    </div>
    <div class="movie-list q-mr-md">
      <MovieList :parametersFilter="filtros" />
    </div>
  </div>
</template>

<style>
.movie-page {
  display: flex;
  justify-content: space-between;
}

.movie-filter {
  width: 25%;
}

.movie-list {
  width: 75%;
}
</style>

<script>
import MovieFilter from "src/components/movie/MovieFilter.vue";
import MovieList from "src/components/movie/MovieList.vue";

export default {
  name: "MoviePage",
  components: { MovieFilter, MovieList },
  data() {
    return {
      filtros: {
        ptsMin: 0,
        qVoteMin: 0,
      },
    };
  },
  methods: {
    actualizarFiltros(prm) {
      this.filtros = prm;
    },
  },
};
</script>
