<template lang="">
    <header>
      <h1>Panier | Shopping Cart App</h1>
    </header>
</template>

<style scoped>
  header {
    background: var(--accent-color);
    color: var(--primary-color);
    padding: 1rem;
  }
  header h1 {
    text-align: center;
    margin: 0;
    font-size: x-large;
    font-weight: bolder;
  }
</style>

<script lang="ts">

import Vue from "vue";
export default Vue.extend({
  name: "Header",
});

</script>
