<template>
  <div class="my-header p-4 bg-dark mb-3">
    <nav class="navbar navbar-light">
      <div class="d-flex justify-content-between align-items-center">
        <div>
          <img src="https://1000marche.net/wp-content/uploads/2020/03/Netflix-Logo-2006.png" alt="Netflix Logo">
        </div>
        <div>
          <input v-model="inputSearch" @keyup.enter="sendInputSearch(inputSearch)" class="me-2" type="text" placeholder="Cerca Film o Serie TV">
          <button @click="sendInputSearch(inputSearch)" class="btn" type="text">Cerca</button>
        </div>
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
  .my-header {
    margin-bottom: 0 !important;
    .navbar {
      div {
        width: 100%;
        div {
          img {
            width: 100px;
          }
        }
        div {
          width: 22rem;
          button {
            background-color: #E50914;
            color: white;
            padding: .3rem 2rem;
          }
        }
      }
    }
    
  }
</style>