<template>
  <section class="container">
    <div class="row">
      <div
        class="col-sm-6 col-md-3 col-xl-2"
        v-for="(movie, index) in searchAll"
        :key="index"
      >
        <card-component :item="movie" />
      </div>
    </div>
  </section>
</template>

<script>
import { state } from "../store.js";
import CardComponent from "./CardComponent.vue";

export default {
  name: "GridList",
  components: { CardComponent },
  computed: {
    searchAll() {
      return state.searchAll;
    },
  },
};
</script>

<style lang="scss">
@import '../styles/general.scss'; 
</style>
