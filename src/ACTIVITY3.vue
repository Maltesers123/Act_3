<template>
    <div id="app">
      <h1>Vue.js Shopping Cart</h1>
      
      <!-- Product list -->
      <div v-if="products.length > 0">
        <div class="product-container" v-for="product in products" :key="product.id">
          <h3>{{ product.name }}</h3>
          <p>Price: ${{ product.price }}</p>
          <button @click="addToCart(product)" class="add-to-cart">Add to Cart</button>
        </div>
      </div>
      <div v-else>
        <p>No products available.</p>
      </div>
  
      <!-- Shopping cart -->
      <div>
        <h2>Shopping Cart</h2>
        <div v-if="cart.length === 0">
          <p>Your cart is empty.</p>
        </div>
        <div class="cart-item" v-for="item in cart" :key="item.id">
          {{ item.name }} - ${{ item.price }} x {{ item.quantity }}
          <button @click="removeFromCart(item)" class="remove">Remove</button>
          <button @click="incrementItem(item)" class="increment">+</button>
          <button @click="decrementItem(item)" class="decrement">-</button>
        </div>
        <p>Total: ${{ getTotalPrice() }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [
          { id: 1, name: 'Yakult', price: 10 },
          { id: 2, name: 'Coke Mismo', price: 20 },
          { id: 3, name: 'DingDong', price: 30 },
          { id: 4, name: 'Yumburger', price: 40 },
          { id: 5, name: 'Chicken Burger', price: 50 },
          { id: 6, name: 'Spaghetti', price: 60 },
          { id: 7, name: 'Iced americano', price: 70 },
          { id: 8, name: 'Iced caramel macchiato', price: 80 },
          { id: 9, name: 'Iced cappuccino', price: 90 },
          { id: 10, name: 'Chicken with Spaghetti', price: 100 },
        ],
        cart: []
      };
    },
    methods: {
      addToCart(product) {
        const existingItem = this.cart.find(item => item.id === product.id);
        if (existingItem) {
          existingItem.quantity++;
        } else {
          this.cart.push({
            id: product.id,
            name: product.name,
            price: product.price,
            quantity: 1
          });
        }
      },
      removeFromCart(item) {
        const index = this.cart.indexOf(item);
        if (index !== -1) {
          this.cart.splice(index, 1);
        }
      },
      incrementItem(item) {
        item.quantity++;
      },
      decrementItem(item) {
        if (item.quantity > 1) {
          item.quantity--;
        }
      },
      getTotalPrice() {
        return this.cart.reduce((total, item) => total + (item.price * item.quantity), 0);
      }
    }
  };
  </script>
  
  <style scoped>
  #app {
    font-family: Arial, sans-serif;
    max-width: 600px;
    margin: 0 auto;
  }
  .product-container {
    margin-bottom: 20px;
    border-bottom: 1px solid #ccc;
    padding-bottom: 10px;
  }
  .product-container button.add-to-cart {
    margin-top: 5px;
    background-color: green;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  .product-container button:hover {
    background-color: darkgreen;
  }
  .cart-item {
    margin-bottom: 10px;
    padding-bottom: 5px;
    border-bottom: 1px solid #ccc;
  }
  .cart-item button.remove {
    margin-left: 10px;
    background-color: red;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  .cart-item button.increment {
    background-color: green;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  .cart-item button.decrement {
    background-color: red;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  .cart-item button.decrement:hover {
    background-color: darkred;
  }
  .cart-item button.remove:hover {
    background-color: darkred;
  }
  .cart-item button.increment:hover {
    background-color: darkgreen;
  }
  </style>
  
