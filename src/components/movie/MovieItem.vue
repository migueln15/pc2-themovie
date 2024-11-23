<template>
  <q-card class="movie-card">
    <q-card-section>
      <q-img
        :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
        alt="Imagen del producto"
      />
    </q-card-section>
    <q-card-section>
      <q-card-title>{{ movie.original_title }}</q-card-title>
      <div class="font-weight-bold">
        Puntuación promedios: {{ movie.vote_average }}
      </div>
      <div class="font-weight-bold">
        Total de votaciones: {{ movie.vote_count }}
      </div>
      <div class="text-center">
        <q-btn color="primary" label="Agregar"></q-btn>
      </div>
    </q-card-section>
  </q-card>
</template>

<style>
.movie-card {
  width: 300px;
}
.movie-card q-card-section {
  height: 100px;
  overflow: hidden;
}
</style>

<script>
export default {
  name: "MovieItem",
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {};
  },
};
</script>
