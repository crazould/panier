<template>
  <div>
    <header>
      <h1>Panier - Shopping Cart App</h1>
    </header>
    <main>

    </main>
    <footer>© {{ year }} Thariq, All right reserved</footer>
  </div>
</template>

<style scoped>
  main{
    min-height: 90vh;
  }
</style>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "IndexPage",
  computed: {
    year() {
      return new Date().getFullYear();
    },
  },
  data() {
    return {};
  },
});
</script>
