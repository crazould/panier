<template lang="">
  <footer>
    © {{ new Date().getFullYear() }} Thariq, All right reserved
  </footer>
</template>

<style scoped>
  footer {
    background: var(--accent-color);
    color: var(--primary-color);
    padding: 1rem;
    text-align: center;
  }
</style>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "Footer",
});
</script>
