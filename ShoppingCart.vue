<template>
    <div>
      <h1 style="color: violet;">Shopping Cart</h1>
      <div>
        <h2 style="color: violet;">Products</h2>
        <ul>
          <li v-for="(product, index) in products" :key="index">
            {{ product.name }} - ₱{{ product.price }}
            <button  style="background-color: violet;" @click="addToCart(index)">Add to Cart</button>
          </li>
        </ul>
      </div>
      <div>
        <h2 style="color: violet;">Cart</h2>
        <ul>
          <li v-for="(item, index) in cart" :key="index">
            {{ item.name }} - ₱{{ item.price }} - Quantity: {{ item.quantity }}
            <button @click="removeFromCart(index)">Remove</button>
            <button @click="increaseQuantity(index)">+</button>
            <button @click="decreaseQuantity(index)">-</button>
          </li>
        </ul>
        <p>Total: ₱{{ total }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [
          { name: 'Pizza', price: 100 },
          { name: 'Burger', price: 130 },
          { name: 'Wings', price: 160 },
          { name: 'Fried Chicken', price: 85 },
          { name: 'Takoyaki', price: 115 },
          { name: 'Siomai', price: 40 }
        ],
        cart: []
      };
    },
    computed: {
      total() {
        return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
      }
    },
    methods: {
      addToCart(index) {
        const productToAdd = this.products[index];
        const existingItemIndex = this.cart.findIndex((item) => item.name === productToAdd.name);
        if (existingItemIndex !== -1) {
          this.cart[existingItemIndex].quantity++;
        } else {
          this.cart.push({ ...productToAdd, quantity: 1 });
        }
      },
      removeFromCart(index) {
        this.cart.splice(index, 1);
      },
      increaseQuantity(index) {
        this.cart[index].quantity++;
      },
      decreaseQuantity(index) {
        if (this.cart[index].quantity > 1) {
          this.cart[index].quantity--;
        }
      }
    }
  };
  </script>
  <style>
   ul{list-style-type: none;}
</style>