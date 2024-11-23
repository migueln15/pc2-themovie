<template>
  <h6>Filtros</h6>
  <div class="vote-filter">
    <q-form @submit.prevent="ActualizarBusqueda" ref="loginForm">
      <label>Votaciones</label>
      <q-input
        class="vote"
        v-model="ptsMin"
        filled
        type="number"
        label="Puntuación Mínima"
      />
      <q-input
        class="vote"
        v-model="qVoteMin"
        filled
        type="number"
        label="Votaciones Mínima"
      />
      <!-- Botón de inicio de sesión -->
      <q-btn
        label="Aplicar filtros"
        color="primary"
        class="q-mt-lg full-width"
        type="submit"
      />
    </q-form>
  </div>
</template>

<style></style>

<script>
export default {
  name: "MovieFilter",
  emits: ["parametersChange"],
  data() {
    return {
      ptsMin: 0,
      qVoteMin: 0,
    };
  },
  mounted() {},
  methods: {
    ActualizarBusqueda() {
      this.$emit("parametersChange", {
        ptsMin: this.ptsMin,
        qVoteMin: this.qVoteMin,
      });
    },
  },
};
</script>
