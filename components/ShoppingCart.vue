<template>
  <div>
    <h3>Shopping Cart</h3>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>QTY</th>
          <th>Price</th>
          <th>Sub total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="cart in carts" :key="cart.product.id">
          <td>{{ cart.product.title }}</td>
          <td>{{ cart.quantity }}</td>
          <td>{{ cart.product.price }}</td>
          <td>{{ cart.quantity * cart.product.price }}</td>
        </tr>
      </tbody>
    </table>
    <button v-on:click="checkout">Checkout</button>
  </div>
</template>

<style scoped></style>

<script lang="ts">
import Vue, { PropType } from "vue";
import { Product } from "./ProductList.vue";

export interface Cart {
  product: Product;
  quantity: number;
}

export default Vue.extend({
  name: "ShoppingCart",
  props: {
    carts: {
      type: Array as PropType<Cart[]>,
      required: true,
    },
  },
  methods: {
    checkout() {
      if (this.carts.length === 0) return;
      this.carts.splice(0, this.carts.length);
    },
  },
});
</script>
