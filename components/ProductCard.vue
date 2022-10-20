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
      <p class="desc">
        {{
          product.description.length >= 54
            ? `${product.description.substring(0, 54)}...`
            : product.description
        }}
      </p>
      <p class="disc-price">
        {{
          `$${Math.round(
            product.price - (product.price * product.discountPercentage) / 100
          )}`
        }}
      </p>
      <div class="discount">
        <span class="percentage">{{ `${product.discountPercentage}%` }}</span>
        <span class="price">{{ `$${product.price}` }}</span>
      </div>
      <div class="rating">
        {{ `${product.rating}` }}
      </div>
    </div>
    <div class="card-footer">
      <button class="add-btn" v-on:click="addToCart(product)">
        Add To Cart
      </button>
    </div>
  </li>
</template>

<style scoped>
.card {
  box-shadow: 0px 15px 50px rgba(108, 146, 181, 0.15);
  border-radius: 25px;
  width: 376px;
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
  }
});
</script>
