<template>
  <div>
    <Header />
    <main>
      {{products}}
    </main>
    <Footer />
  </div>
</template>

<style scoped>

</style>

<script lang="ts">
import Vue from "vue";
import Header from "../components/Header.vue"
import Footer from "../components/Footer.vue"

export default Vue.extend({
  name: "IndexPage",
  components: {
    Header,
    Footer
  },
  data: () => ({
    products: [],
  }),
  async fetch() {
    this.products = await fetch("https://dummyjson.com/products").then(
      (res) => res.json()
    );
  },
});
</script>
