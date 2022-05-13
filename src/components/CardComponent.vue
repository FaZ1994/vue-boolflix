<template>
  <div class="card-container align-item-center">
    <img
      class="img-fluid h-100 w-100"
      :src="imgSRC + item.poster_path"
      alt=""
    />
    <div class="text-box">
      <span>Titolo: {{ item.title ? item.title : item.name }}</span>
      <span
        >Titolo originale:
        {{
          item.original_title ? item.original_title : item.original_name
        }}</span
      >
      <span
        >Paese di produzione: <country-flag :country="language" size="small" />
      </span>
      <span
        >Voto:
        <span v-for="(n, index) in 5" :key="index">
          <i
            :class="n <= ratingMath ? 'fa-solid fa-star' : 'fa-regular fa-star'"
          ></i>
        </span>
      </span>
      <span>Overview: {{ item.overview }} </span>
    </div>
  </div>
  <!--  
          titolo originale: {{item.original_title ? item.original_title : item.original_name}}<br />
          titolo: {{item.title ? item.title : item.name}}<br />
          lingua: <country-flag :country='language' size='small'/><br />
          voto: <span v-for="(n,index) in 5" :key="index">
              <i :class="n <= ratingMath ? 'fa-solid fa-star' : 'fa-regular fa-star'"></i>
          </span>
          
           <i v-for="index in ratingMath(item.vote_average)" :key="index" class="fa-solid fa-star"></i>
          <span v-if="item.vote_average === 0"><i class="fa-regular fa-star"></i></span> -->
</template>

<script>
import CountryFlag from "vue-country-flag";

export default {
  name: "CardComponent",
  components: {
    CountryFlag,
  },
  props: ["item"],
  data() {
    return {
      imgSRC: "https://image.tmdb.org/t/p/w342/",
    };
  },

  computed: {
    language() {
      if (this.item.original_language === "en") {
        return "gb";
      } else if (this.item.original_language === "ja") {
        return "jp";
      } else {
        return this.item.original_language;
      }
    },

    ratingMath() {
      return Math.ceil(this.item / 2);
    },
  },
};
</script>

<style lang="scss">
@import "../styles/general.scss";
</style>
