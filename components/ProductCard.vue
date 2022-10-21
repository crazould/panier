<template>
  <li class="card" :key="product.id">
    <div class="card-header">
      <div class="thumbnail-wrapper">
        <img
          class="thumbnail"
          :src="product.thumbnail"
          :alt="`${product.title} thumbnail image`"
        />
      </div>
      <p class="category">{{ product.category }}</p>
    </div>
    <div class="card-body">
      <h2 class="name">{{ product.title }}</h2>
      <p class="desc">{{ productDesc }}</p>
      <p class="disc-price">{{ productDiscPrice }}</p>
      <div class="discount">
        <span class="percentage">{{ `${product.discountPercentage}%` }}</span>
        <span class="price">{{ `$${product.price}` }}</span>
      </div>
      <div class="rating">
        <svg
          width="17"
          height="16"
          viewBox="0 0 17 16"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M0.549458 5.63406L5.64573 4.90408L7.92389 0.352135C7.98612 0.227506 8.08848 0.126615 8.21494 0.0652895C8.53207 -0.0890138 8.91746 0.0395723 9.07603 0.352135L11.3542 4.90408L16.4505 5.63406C16.591 5.65384 16.7194 5.71912 16.8178 5.81803C16.9367 5.93848 17.0022 6.10053 16.9999 6.26856C16.9977 6.4366 16.9278 6.59688 16.8057 6.71418L13.1185 10.2572L13.9896 15.2602C14.0101 15.3766 13.997 15.4963 13.9519 15.6057C13.9068 15.7151 13.8315 15.8099 13.7346 15.8793C13.6376 15.9488 13.5229 15.99 13.4033 15.9984C13.2838 16.0068 13.1643 15.982 13.0583 15.9269L8.49996 13.5648L3.94162 15.9269C3.81717 15.9922 3.67265 16.0139 3.53416 15.9902C3.1849 15.9308 2.95006 15.6044 3.01028 15.2602L3.8814 10.2572L0.194184 6.71418C0.0938245 6.61724 0.0275873 6.49064 0.00751532 6.35216C-0.046679 6.00597 0.198199 5.68549 0.549458 5.63406Z"
            fill="#FFC226"
          />
        </svg>
        {{ `${product.rating}` }}
      </div>
    </div>
    <div class="card-footer">
      <div v-if="addedCart.quantity" class="quantity-group">
        <button v-on:click="decreaseQuantity()">-</button>
        <span>{{ addedCart.quantity }}</span>
        <button v-on:click="increaseQuantity()">+</button>
      </div>
      <button v-else class="add-btn" v-on:click="addToCart(product)">
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
        Add To Cart
      </button>
    </div>
  </li>
</template>

<style scoped>
.card {
  box-shadow: 0px 15px 50px rgba(108, 146, 181, 0.15);
  border-radius: 25px;
  display: block;
}

.card-body {
  padding: 22px 24px;
}

.thumbnail-wrapper {
  height: 253px;
  overflow: hidden;
  border-radius: 25px 25px 0px 0px;
  display: flex;
  justify-content: center;
}

.thumbnail {
  height: 100%;
}

.category {
  background: var(--accent-color);
  border-radius: 0px 0px 45px 0px;
  color: var(--primary-color);
  padding: 0.75rem 1.5rem;
  font-family: "Poppins";
  text-transform: capitalize;
}

.name {
  font-family: "Roboto";
  font-weight: 500;
  font-size: 18px;
  color: var(--muted-color);
  margin-bottom: 15px;
  text-transform: uppercase;
  text-overflow: ellipsis;
  overflow-x: hidden;
  white-space: nowrap;
}

.desc {
  font-family: "Roboto";
  font-weight: 600;
  font-size: 22px;
  color: var(--secondary-color);
  margin-bottom: 25px;
}

.disc-price {
  font-style: normal;
  font-weight: 600;
  font-size: 26px;
  font-family: "Poppins";
  margin-bottom: 15px;
}

.discount {
  margin-bottom: 19px;
}

.discount .percentage {
  font-family: "Roboto";
  color: var(--danger-color);
  padding: 5px;
  background: #ffdbe2;
  border-radius: 4px;
  font-weight: 600;
  margin-right: 0.25rem;
}

.discount .price {
  font-family: "Roboto";
  color: var(--muted-color);
  text-decoration: line-through;
}

.rating {
  color: var(--warning-color);
  font-family: "Roboto";
}

.card-footer {
  padding-inline: 22px;
  padding-bottom: 43px;
  padding-top: 15px;
}

.add-btn {
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
}
</style>

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
  name: "ProductCard",
  props: {
    product: {
      type: Object as PropType<Product>,
      required: true,
    },
    carts: {
      type: Array as PropType<Cart[]>,
      required: true,
    },
  },
  computed: {
    productDesc() {
      return this.product.description.length >= 34
        ? `${this.product.description.substring(0, 34)}...`
        : this.product.description;
    },
    productDiscPrice() {
      return `$${Math.round(
        this.product.price -
          (this.product.price * this.product.discountPercentage) / 100
      )}`;
    },
    addedCart() {
      const addedCart = this.carts.find(
        (cart) => cart.product.id === this.product.id
      );
      if (addedCart) return addedCart;
      else return { product: null, quantity: 0 };
    },
    addedCartIdx() {
      return this.carts.findIndex(
        (cart) => cart.product.id === this.product.id
      );
    },
  },
  data: () => ({}),
  methods: {
    addToCart(product: Product) {
      this.carts.push({
        product,
        quantity: 1,
      });
    },
    increaseQuantity() {
      this.addedCart.quantity += 1;
      this.carts.map((cart) => {
        if (
          this.addedCart.product &&
          cart.product.id === this.addedCart.product.id
        )
          return this.addedCart;
        else return cart;
      });
    },
    decreaseQuantity() {
      this.addedCart.quantity -= 1;
      if (this.addedCart.quantity > 0) {
        this.carts.map((cart) => {
          if (
            this.addedCart.product &&
            cart.product.id === this.addedCart.product.id
          )
            return this.addedCart;
          else return cart;
        });
      } else {
        this.carts.splice(this.addedCartIdx, 1);
      }
    },
  },
});
</script>
