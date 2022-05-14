<template>
  <div class="card-container border border-light align-item-center">
    <img
      class="img-fluid h-100 w-100"
      :src="imgLogic"
      alt="poster not found"
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
            :class="
              n <= ratingMath
                ? 'fa-solid fa-star gold'
                : 'fa-regular fa-star gold'
            "
          ></i>
        </span>
      </span>
      <span>Overview: {{ item.overview }} </span>
    </div>
  </div>
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
      return Math.ceil(this.item.vote_average / 2);
    },

    imgLogic(){
          let imgSRC = "https://image.tmdb.org/t/p/w342/";
            if((imgSRC + this.item.poster_path) === (imgSRC + null)){
                return 'https://critics.io/img/movies/poster-placeholder.png'
            }else{
                return imgSRC + this.item.poster_path 
            }
  },
  }
};
</script>

<style lang="scss">
@import "../styles/general.scss";

.gold {
  color: rgb(226, 204, 1);
}


.card-container {
  min-width: 200px;
  height: 260px;
  margin: 2em;
  position: relative;
  overflow-y: auto;
  position: relative;

  .text-box {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    display: none !important;
    padding: .5em;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.5);
  }
  &:hover .text-box {
    display: block !important;
  }
}
</style>
