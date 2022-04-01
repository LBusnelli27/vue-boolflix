<template>
  <div>
    <div class="row">
      <div class="col-3 px-4">
        <h3>Titolo</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            {{ element.title }}
          </li>
        </ul>
      </div>

      <div class="col-3 px-4">
        <h3>Titolo originale</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            {{ element.original_title }}
          </li>
        </ul>
      </div>

      <div class="col-3 px-4">
        <h3>Lingua</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            <img class="my-lang-flag" v-if="element.original_language == 'it'" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Bandiera_italiana_foto.svg/2560px-Bandiera_italiana_foto.svg.png" alt="Bandiera italiana">
            <img class="my-lang-flag" v-if="element.original_language == 'en'" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Flag_of_the_United_Kingdom.svg/1200px-Flag_of_the_United_Kingdom.svg.png" alt="Bandiera inglese">
            <img class="my-lang-flag" v-if="element.original_language == 'fr'" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Flag_of_France.svg/280px-Flag_of_France.svg.png" alt="Bandiera fracese">
            <img class="my-lang-flag" v-if="element.original_language == 'de'" src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/2560px-Flag_of_Germany.svg.png" alt="Bandiera tedesca">
            <span v-if="element.original_language != 'it' & element.original_language != 'en' & element.original_language != 'fr' & element.original_language != 'de'">{{ element.original_language }}</span>
          </li>
        </ul>
      </div>

      <div class="col-3 px-4">
        <h3>Voto</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            {{ element.vote_average }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name : 'MainComponent',

  data() {
    return {
      listOfSearched : []
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
      .then(response => (this.listOfSearched = response.data.results));
    }
  },
}
</script>

<style lang="scss" scoped>
  li {
    .my-lang-flag {
      width: 30px;
      height: 20px;
    }
  }
</style>