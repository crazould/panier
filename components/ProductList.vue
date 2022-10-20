<template>
  <ul>
    <li v-for="product in products" :key="product.id">
      <strong>{{ product.title }}</strong>
      <em>${{ product.price }}</em>
      <button v-on:click="addToCart(product)">+</button>
    </li>
  </ul>
</template>

<style scoped></style>

<script lang="ts">
import Vue, { PropType } from "vue";
import { Cart } from "./ShoppingCart.vue";

export interface Product {
  id: string;
  title: string;
  description: string;
  price: number;
  discountPercentage: number;
  brand: string;
  rating: number;
  category: string;
  thumbnail: string;
  images: string[];
}

export default Vue.extend({
  name: "ProductList",
  props: {
    products: {
      type: Array as PropType<Product[]>,
      required: true,
    },
    carts: {
      type: Array as PropType<Cart[]>,
      required: true,
    },
  },
  methods: {
    addToCart(product: Product) {
      const oldCart = this.carts.find((cart) => cart.product.id === product.id);
      if (oldCart) {
        oldCart.quantity += 1;
        this.carts.map((cart) => {
          if (cart.product.id === oldCart.product.id) return oldCart;
          else return cart;
        });
      } else if (!oldCart) {
        this.carts.push({
          product,
          quantity: 1,
        });
      }
    },
  },
});
</script>
