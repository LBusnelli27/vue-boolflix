<template>
  <div class="p-4 bg-dark mb-3">
    <nav class="navbar navbar-light">
      <div class="d-flex">
          <input v-model="inputSearch" @keyup.enter="sendInputSearch(inputSearch)" class="me-2" type="text" placeholder="Cerca Film o Serie TV">
          <button @click="sendInputSearch(inputSearch)" class="btn btn-success" type="text">Cerca</button>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name : 'HeaderComponent',

  data() {
    return {
      inputSearch : '',
    }
  },

  methods: {
    sendInputSearch(msgToSend) {
      this.$root.$emit('search', msgToSend);
      this.inputSearch = '';
    }
  },
}
</script>

<style  lang="scss" scoped>

</style>