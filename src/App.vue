<template>
  <div id="app">
    <!-- menggunakan route name -->
    <nav><router-link :to="{ name: 'product' }">Product</router-link> | <router-link to="/product/">Home</router-link> |</nav>
    <nav><router-link :to="{ name: 'productDetail', params: { id: 22 } }">Detail Product</router-link> | <router-link to="/product/">Home</router-link> |</nav>
    <nav><router-link :to="{ name: 'cart' }">Cart</router-link> | <router-link to="/product/">Home</router-link> |</nav>
    <router-view />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
  font-family: Arial;
}

#page-wrap {
  margin: auto;
  max-width: 800px;
  min-height: 100vh;
}

button {
  background-color: #41b883;
  border: none;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  outline: 0;
  padding: 16px;
}
</style>
