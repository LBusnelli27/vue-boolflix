<template>
  <div>
    <div class="row">
      <div class="col-12 d-flex p-5">
        <input class="me-2" type="text">
        <button class="btn btn-primary">Search</button>
      </div>
      <div class="col-12">
        <ul></ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name : 'MainComponent',

  mounted () {
    axios
      .get('https://api.themoviedb.org/3/movie/550?api_key=8e367e7bbe971330f3e274f6b4bddf1e')
      .then(response => (this.albumList = response.data.response));
  }
}
</script>

<style>
  
</style>