<template>
  <div>
    <div class="row">
      <div class="col-12 d-flex p-5">
        <input v-model="inputSearch" @keyup.enter="searchApiTheMovie()" class="me-2" type="text">
        <button @click="searchApiTheMovie()" class="btn btn-primary">Search</button>
      </div>
      <div class="col-3 px-4">
        <h3>Title</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            {{ element.title }}
          </li>
        </ul>
      </div>
      <div class="col-3 px-4">
        <h3>Original Title</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            {{ element.original_title }}
          </li>
        </ul>
      </div>
      <div class="col-3 px-4">
        <h3>Language</h3>
        <ul>
          <li class="mb-2" v-for="(element, index) in listOfSearched" :key="index">
            {{ element.original_language }}
          </li>
        </ul>
      </div>
      <div class="col-3 px-4">
        <h3>Vote</h3>
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
      inputSearch : '',
      listOfSearched : []
    }
  },

  methods: {
    searchApiTheMovie() {
      axios
      .get('https://api.themoviedb.org/3/search/movie?api_key=8e367e7bbe971330f3e274f6b4bddf1e&query=' + this.inputSearch.replace(/\s/g , "+"))
      .then(response => (this.listOfSearched = response.data.results));
    }
  }
}
</script>

<style>
  
</style>