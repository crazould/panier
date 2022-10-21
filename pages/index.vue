<template>
  <div>
    <Header></Header>
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
    <Footer></Footer>
  </div>
</template>

<style scoped>
.wrapper {
  margin: auto;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.product-list {
  display: grid;
  grid-template-columns: repeat(1, minmax(0, 1fr));
  max-width: calc(376px * 4 + 40px * 3);
  grid-gap: 36px;
}

@media screen and (min-width: 768px) {
  .product-list {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media screen and (min-width: 1024px) {
  .product-list {
    grid-template-columns: repeat(3, minmax(0, 1fr));
    grid-gap: 24px;
  }
}

@media screen and (min-width: 1440px) {
  .product-list {
    grid-template-columns: repeat(4, minmax(0, 1fr));
  }
  .wrapper {
    padding-block: 2rem;
    flex-direction: row-reverse;
    justify-content: center;
    align-items: flex-start;
  }
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
