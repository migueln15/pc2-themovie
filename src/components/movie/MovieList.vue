<template>
  <h5>Listado de Peliculas</h5>
  <div class="movie-list">
    <div class="movie-grid">
      <div class="movie-item" v-for="item in movies" :key="item.id">
        <MovieItem :movie="item" />
      </div>
    </div>
  </div>
</template>

<style>
.movie-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
}
</style>

<script>
import MovieItem from "./MovieItem.vue";

export default {
  name: "MovieList",
  components: { MovieItem },
  computed: {},
  props: {
    parametersFilter: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      movies: [],
    };
  },
  mounted() {
    this.cargarPeliculas();
  },
  watch: {
    parametersFilter: {
      handler() {
        this.cargarPeliculas();
      },
      deep: true,
    },
  },
  methods: {
    cargarPeliculas() {
      const endpointURL = `https://api.themoviedb.org/3/discover/movie?include_adult=true&include_video=false&language=en-US&page=1&sort_by=popularity.desc&vote_average.gte=${this.parametersFilter.ptsMin}&vote_count.gte=${this.parametersFilter.qVoteMin}`;
      const token =
        "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJiMmUwOTE3MTE5ZTIwNWZlY2I2ODViMzI1MGFlMWJmMiIsIm5iZiI6MTczMjMzMzUwMC4wOTk1NTQ1LCJzdWIiOiI2NzQxNGQ3ZTRhM2RjMTc4MTczZDRjNjMiLCJzY29wZXMiOlsiYXBpX3JlYWQiXSwidmVyc2lvbiI6MX0.r71tFf5VYEuhNLjZUU8vY-cg4xd0H0ooj15UiMBxuio";

      this.$axios
        .get(endpointURL, {
          headers: {
            Authorization: `Bearer ${token}`,
            Accept: "application/json",
          },
        })
        .then((response) => {
          this.movies = response.data.results;
          console.log(response);
        })
        .catch((error) => {
          console.error("Error al cargar las películas:", error);
        });
    },
  },
};
</script>
