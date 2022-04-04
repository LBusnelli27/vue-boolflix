<template>
  <div class="my-bg-main p-5">
    <Card />
  </div>
</template>

<script>
import Card from './Card.vue';

export default {
  name : 'MainComponent',

  components: {
    Card
  },
}
</script>

<style lang="scss" scoped>
  .my-bg-main {
    background-color: rgb(98, 98, 98);
  }
  li {
    .my-lang-flag {
      width: 30px;
      height: 20px;
    }
  }
</style>