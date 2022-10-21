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
    <div v-if="!carts.length" class="empty-cart">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="198px"
        height="192px"
        viewBox="0 0 197 192"
        version="1.1"
      >
        <g id="surface1">
          <path
            style="
              stroke: none;
              fill-rule: evenodd;
              fill: #b6b6b6;
              fill-opacity: 1;
            "
            d="M 49.121094 16 L 11.003906 16 L 11.003906 32 L 36.601562 32 L 58.632812 133.425781 L 58.726562 133.425781 L 58.726562 136 L 162.132812 136 L 162.132812 134.015625 L 179.578125 56.726562 L 182.265625 48 L 55.984375 48 L 51.449219 27.113281 Z M 162.03125 64 L 59.460938 64 L 71.621094 120 L 149.390625 120 Z M 162.03125 64 "
          />
          <path
            style="
              stroke: none;
              fill-rule: nonzero;
              fill: #b6b6b6;
              fill-opacity: 1;
            "
            d="M 82.59375 176 C 86.8125 176 90.859375 174.3125 93.839844 171.3125 C 96.824219 168.3125 98.5 164.246094 98.5 160 C 98.5 155.753906 96.824219 151.6875 93.839844 148.6875 C 90.859375 145.6875 86.8125 144 82.59375 144 C 78.375 144 74.324219 145.6875 71.34375 148.6875 C 68.359375 151.6875 66.683594 155.753906 66.683594 160 C 66.683594 164.246094 68.359375 168.3125 71.34375 171.3125 C 74.324219 174.3125 78.375 176 82.59375 176 Z M 154.179688 160 C 154.179688 164.246094 152.503906 168.3125 149.519531 171.3125 C 146.539062 174.3125 142.492188 176 138.273438 176 C 134.054688 176 130.003906 174.3125 127.023438 171.3125 C 124.039062 168.3125 122.363281 164.246094 122.363281 160 C 122.363281 155.753906 124.039062 151.6875 127.023438 148.6875 C 130.003906 145.6875 134.054688 144 138.273438 144 C 142.492188 144 146.539062 145.6875 149.519531 148.6875 C 152.503906 151.6875 154.179688 155.753906 154.179688 160 Z M 154.179688 160 "
          />
        </g>
      </svg>
    </div>
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
    <button v-if="carts.length" class="checkout-btn" v-on:click="checkout()">
      <svg
        width="35"
        height="34"
        viewBox="0 0 35 34"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        style="margin-right: 17px"
      >
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M8.70529 2.83334H1.91663V5.66668H6.47546L10.3996 23.6272H10.4166V24.0833H28.8333V23.732L31.94 10.0456L32.4189 8.50001H9.92788L9.12038 4.80109L8.70529 2.83334ZM28.8149 11.3333H10.547L12.713 21.25H26.5638L28.8149 11.3333Z"
          fill="white"
        />
        <path
          d="M14.6667 31.1667C15.4182 31.1667 16.1388 30.8682 16.6702 30.3368C17.2015 29.8054 17.5 29.0848 17.5 28.3333C17.5 27.5819 17.2015 26.8612 16.6702 26.3299C16.1388 25.7985 15.4182 25.5 14.6667 25.5C13.9153 25.5 13.1946 25.7985 12.6632 26.3299C12.1319 26.8612 11.8334 27.5819 11.8334 28.3333C11.8334 29.0848 12.1319 29.8054 12.6632 30.3368C13.1946 30.8682 13.9153 31.1667 14.6667 31.1667ZM27.4167 28.3333C27.4167 29.0848 27.1182 29.8054 26.5868 30.3368C26.0555 30.8682 25.3348 31.1667 24.5834 31.1667C23.8319 31.1667 23.1113 30.8682 22.5799 30.3368C22.0486 29.8054 21.75 29.0848 21.75 28.3333C21.75 27.5819 22.0486 26.8612 22.5799 26.3299C23.1113 25.7985 23.8319 25.5 24.5834 25.5C25.3348 25.5 26.0555 25.7985 26.5868 26.3299C27.1182 26.8612 27.4167 27.5819 27.4167 28.3333Z"
          fill="white"
        />
      </svg>
      Checkout
    </button>
  </div>
</template>

<style scoped>
.shopping-cart {
  background: #ffffff;
  box-shadow: 0px 15px 50px rgba(108, 146, 181, 0.1);
  border-radius: 25px;
  padding: 56px 42px;
  margin-bottom: 40px;
}

@media screen and (min-width: 1440px) {
  .shopping-cart {
    margin-left: 24px;
    margin-bottom: 0px;
  }
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
  padding-top: 50px;
  border-top: 1px solid #e3e3e3;
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

.empty-cart {
  display: flex;
  justify-content: center;
  align-items: center;
}

.checkout-btn {
  margin-top: 63px;
  padding-block: 1.1rem;
  width: 100%;
  background: var(--accent-color);
  color: var(--primary-color);
  font-weight: 700;
  font-size: 18px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  box-shadow: 0 25px 25px -12px rgb(1 172 196 / 0.25);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: 250ms;
}

.checkout-btn:hover {
  box-shadow: 0 25px 25px 0px rgb(1 172 196 / 0.3);
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
