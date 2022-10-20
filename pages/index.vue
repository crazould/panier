<template>
  <div>
    <Header />
    <main>
      <div class="wrapper">
        <ShoppingCart :carts="carts" />
        <ul class="product-list">
          <ProductCard
            v-for="product in products"
            :key="product.id"
            :product="product"
            :carts="carts"
          />
        </ul>
      </div>
    </main>
    <Footer />
  </div>
</template>

<style scoped>
.wrapper {
  margin: auto;
  padding: 1rem;
}
.product-list {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  grid-gap: 40px;
  column-gap: 40px;
  max-width: calc(376px * 4 + 40px * 3);
}
</style>

<script lang="ts">
import Vue from "vue";
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import ShoppingCart, { Cart } from "@/components/ShoppingCart.vue";
import ProductCard, { Product } from "@/components/ProductCard.vue";

interface ProductResponse {
  products: Product[];
  total: number;
  skip: number;
  limit: number;
}

export default Vue.extend({
  name: "IndexPage",
  components: {
    Header,
    Footer,
    ShoppingCart,
    ProductCard,
  },
  data: () => ({
    products: [] as Product[],
    carts: [] as Cart[],
  }),
  async fetch() {
    this.products = await fetch("https://dummyjson.com/products").then(
      async (res) => {
        const data = await (res.json() as Promise<ProductResponse>);
        return data.products;
      }
    );
  },
});
</script>
