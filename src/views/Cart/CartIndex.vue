<template lang="">
  <!-- Elemen utama pembungkus -->
  <div>
    <!-- Kontainer untuk item keranjang belanja -->
    <div id="page-wrap">
      <!-- Judul untuk keranjang belanja -->
      <h1>Shopping Cart</h1>

      <!-- Melakukan loop untuk setiap item dalam cartItems dan membuat kontainer produk -->
      <div class="product-container" v-for="item in cartItems" :key="item.id">
        <!-- Menampilkan gambar produk -->
        <img class="product-image" :src="item.imageUrl" alt="" />

        <!-- Pembungkus untuk detail produk seperti nama dan harga -->
        <div class="details-wrap">
          <!-- Menampilkan nama produk -->
          <h3>{{ item.name }}</h3>
          <!-- Menampilkan harga produk -->
          <p>{{ item.price }}</p>
        </div>

        <!-- Tombol untuk menghapus produk dari keranjang -->
        <button class="remove-button">Remove</button>
      </div>

      <!-- Menampilkan total harga dari semua item dalam keranjang -->
      <h3 id="total-price">Total price: {{ totalPrice }}</h3>

      <!-- Tombol untuk melakukan checkout -->
      <button id="checkout-button">Checkout</button>
    </div>
  </div>
</template>

<script>
// Mengimpor data cartItems dari file 'data-seed'
import { cartItems } from "@/data-seed";

export default {
  // Data yang digunakan dalam komponen ini
  data() {
    return {
      // cartItems berisi array item yang ada di keranjang
      cartItems,
    };
  },
  // Bagian computed untuk menghitung total harga
  computed: {
    totalPrice() {
      // Menghitung total harga dengan menjumlahkan harga setiap item di cartItems
      return this.cartItems.reduce((sumCart, item) => sumCart + Number(item.price), 0).toFixed(2);
    },
  },
};
</script>

<style scoped>
/* Gaya untuk judul */
h1 {
  border-bottom: 1px solid #41b883;
  margin: 0;
  margin-top: 16px;
  padding: 16px;
}
/* Gaya untuk total harga */
#total-price {
  padding: 16px;
  text-align: right;
}
/* Gaya untuk tombol checkout */
#checkout-button {
  width: 100%;
}
/* Gaya untuk kontainer produk */
.product-container {
  align-content: "center";
  border-bottom: 1px solid #ddd;
  display: flex;
  padding: 16px;
  width: 100%;
}
/* Gaya untuk gambar produk */
.product-image {
  flex: 1;
  height: 100px;
  max-width: 100px;
}
/* Gaya untuk detail produk */
.details-wrap {
  padding: 0 16px;
  flex: 3;
}
/* Gaya untuk tombol hapus */
.remove-button {
  flex: 1;
  margin: auto;
}
</style>
