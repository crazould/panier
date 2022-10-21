<template>
  <div class="shopping-cart">
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
          <td>
            ${{
              Math.round(
                cart.product.price -
                  (cart.product.price * cart.product.discountPercentage) / 100
              )
            }}
          </td>
          <td>
            ${{
              cart.quantity *
              Math.round(
                cart.product.price -
                  (cart.product.price * cart.product.discountPercentage) / 100
              )
            }}
          </td>
        </tr>
      </tbody>
    </table>
    <div class="grandtotal">
      <span>Total:</span>
      <span>
        ${{
          carts.reduce((grandTotal, cart) => {
            return (
              grandTotal +
              cart.quantity *
                Math.round(
                  cart.product.price -
                    (cart.product.price * cart.product.discountPercentage) / 100
                )
            );
          }, 0)
        }}</span
      >
    </div>
    <button v-if="carts.length" class="checkout-btn" v-on:click="checkout()">Checkout</button>
  </div>
</template>

<style scoped>
.shopping-cart {
  background: #ffffff;
  box-shadow: 0px 15px 50px rgba(108, 146, 181, 0.1);
  border-radius: 25px;
  padding: 56px 42px;
  width: 480px;
}

h3 {
  margin: 8px 0 40px;
  font-family: "Poppins";
  font-weight: 600;
  font-size: 22px;
}

table {
  min-width: 396px;
  border-spacing: 0 24px;
  border-bottom: 1px solid #e3e3e3;
  margin-bottom: 50px;
}

thead:after {
  content: "";
  display: block;
  height: 3px;
}

th {
  text-align: left;
  font-family: "Roboto";
  font-weight: 600;
  font-size: 18px;
  line-height: 21px;
  color: #7a7d85;
}

td {
  text-transform: capitalize;
  color: var(--muted-color);
}

.grandtotal {
  font-family: "Roboto";
  font-weight: 400;
  font-size: 18px;
  color: #b6b6b6;
  display: flex;
  justify-content: space-between;
}

.grandtotal span:nth-child(2) {
  font-weight: 700;
  font-size: 20px;
  color: #404145;
}

.checkout-btn {
  margin-top: 63px;
  padding-block: 1.1rem;
  width: 100%;
  background: var(--accent-color);
  text-align: center;
  color: var(--primary-color);
  font-weight: 700;
  font-size: 18px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  box-shadow: 0 25px 25px -12px rgb(1 172 196 / 0.25);
}
</style>

<script lang="ts">
import Vue, { PropType } from "vue";
import { Product } from "./ProductCard.vue";

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
  computed: {},
  data: () => ({
    grandTotal: 0,
  }),
  methods: {
    checkout() {
      if (this.carts.length === 0) return;
      this.carts.splice(0, this.carts.length);
    },
  },
});
</script>
