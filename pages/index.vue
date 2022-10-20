<template>
  <div>
    <Header />
    <main>
      <div class="wrapper">
        <ShoppingCart :carts="carts" />
        <ProductList :products="products" :carts="carts" />
      </div>
    </main>
    <Footer />
  </div>
</template>

<style scoped>
  .wrapper{
    max-width: 1280px;
  }
</style>

<script lang="ts">
import Vue from "vue";
import Header from "@/components/Header.vue"
import Footer from "@/components/Footer.vue"
import ProductList, { Product } from "@/components/ProductList.vue"
import ShoppingCart, {Cart} from "@/components/ShoppingCart.vue"

interface ProductResponse {
  products: Product[]
  total: number
  skip: number
  limit: number
}

export default Vue.extend({
  name: "IndexPage",
  components: {
    Header,
    Footer,
    ProductList,
    ShoppingCart,
  },
  data: () => ({
    products: [] as Product[],
    carts: [] as Cart[]
  }),
  async fetch() {
    this.products = await fetch("https://dummyjson.com/products").then(
      async (res) => {
        const data = await (res.json() as Promise<ProductResponse>);
        return data.products
      }
    );
  },
});
</script>
