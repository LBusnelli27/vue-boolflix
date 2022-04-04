<template>
  <div>
    <!-- Film Section -->
    <h2 class="text-center text-uppercase text-white">Film</h2>
    <div class="row row-cols-3 mb-5">
      <div v-for="(element, index) in listOfSearchedFilms" :key="index" class="col">
        <div class="my-card bg-dark">
          <img class="my-thumb-img" :src="'https://image.tmdb.org/t/p/w342' + element.poster_path" :alt="element.original_title + ' image'">
          <div class="p-3">
            <p><span class="fw-bold">Titolo</span> : {{ element.title }}</p>
            <p><span class="fw-bold">Titolo Originale</span> : {{ element.original_title }}</p>
            <p><span class="fw-bold">Lingua</span> : <span class="my-lang-flag "><img class="my-lang-flag" v-if="element.original_language == 'it'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Bandiera_italiana_foto.svg/2560px-Bandiera_italiana_foto.svg.png" alt="Bandiera italiana">
            <img class="my-lang-flag" v-if="element.original_language == 'en'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Flag_of_the_United_Kingdom.svg/1200px-Flag_of_the_United_Kingdom.svg.png" alt="Bandiera inglese">
            <img class="my-lang-flag" v-if="element.original_language == 'fr'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Flag_of_France.svg/280px-Flag_of_France.svg.png" alt="Bandiera fracese">
            <img class="my-lang-flag" v-if="element.original_language == 'de'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/2560px-Flag_of_Germany.svg.png" alt="Bandiera tedesca">
            <span class="text-uppercase" v-if="element.original_language != 'it' & element.original_language != 'en' & element.original_language != 'fr' & element.original_language != 'de'">{{ element.original_language }}</span></span></p>

            <i v-for="(element, index) in voteTranform(element.vote_average)" :key="index" class="fa-solid fa-star"></i>
            <i v-for="(element, index) in 5 - voteTranform(element.vote_average)" :key="index" class="fa-regular fa-star"></i>
          </div>
        </div>
      </div>
    </div>

    <!-- TV Series Section -->
    <h2 class="text-center text-uppercase text-white">Serie TV</h2>
    <div class="row row-cols-3">
      <div v-for="(element, index) in listOfSearchedSeries" :key="index" class="col">
        <div class="my-card bg-dark">
          <img class="my-thumb-img" :src="'https://image.tmdb.org/t/p/w342' + element.poster_path" :alt="element.original_title + ' image'">
          <div class="p-3">
            <p><span class="fw-bold">Titolo</span> : {{ element.name }}</p>
            <p><span class="fw-bold">Titolo Originale</span> : {{ element.original_name }}</p>
            <p><span class="fw-bold">Lingua</span> : <span class="my-lang-flag "><img class="my-lang-flag" v-if="element.original_language == 'it'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Bandiera_italiana_foto.svg/2560px-Bandiera_italiana_foto.svg.png" alt="Bandiera italiana">
            <img class="my-lang-flag" v-if="element.original_language == 'en'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Flag_of_the_United_Kingdom.svg/1200px-Flag_of_the_United_Kingdom.svg.png" alt="Bandiera inglese">
            <img class="my-lang-flag" v-if="element.original_language == 'fr'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Flag_of_France.svg/280px-Flag_of_France.svg.png" alt="Bandiera fracese">
            <img class="my-lang-flag" v-if="element.original_language == 'de'" 
            src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/2560px-Flag_of_Germany.svg.png" alt="Bandiera tedesca">
            <span class="text-uppercase" v-if="element.original_language != 'it' & element.original_language != 'en' & element.original_language != 'fr' & element.original_language != 'de'">{{ element.original_language }}</span></span></p>

            <i v-for="(element, index) in voteTranform(element.vote_average)" :key="index" class="fa-solid fa-star"></i>
            <i v-for="(element, index) in 5 - voteTranform(element.vote_average)" :key="index" class="fa-regular fa-star"></i>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name : 'CardComponent',

    data() {
      return {
        listOfSearchedFilms : [],
        listOfSearchedSeries : [],
      }
    },

    mounted() {
      this.$root.$on('search', (input) => {
        this.searchApiTheMovie(input);
      })
    },

    methods: {
    searchApiTheMovie(inputText) {
      axios
      .get('https://api.themoviedb.org/3/search/movie?api_key=8e367e7bbe971330f3e274f6b4bddf1e&query=' + inputText.replace(/\s/g , "+"))
      .then(response => (this.listOfSearchedFilms = response.data.results));

      axios
      .get('https://api.themoviedb.org/3/search/tv?api_key=8e367e7bbe971330f3e274f6b4bddf1e&query=' + inputText.replace(/\s/g , "+"))
      .then(response => (this.listOfSearchedSeries = response.data.results));
    },

    voteTranform(originalVote) {
      return parseInt(originalVote / 2);
    }
  },
}
</script>

<style lang="scss" scoped>
  .my-card {
    position: relative;
    margin: 1rem;
    width: 342px;
    height: 513px;
    &:hover > img {
      display: none;
    }
    .my-thumb-img {
      position: absolute;
      top: 0;
      left: 0;
    }
    div {
      color: white;
      .my-lang-flag {
      width: 30px;
      height: 20px;
    }
    }
  }
</style>