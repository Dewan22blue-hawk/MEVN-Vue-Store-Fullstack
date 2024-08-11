<template lang="">
  <!-- Elemen utama pembungkus -->
  <div>
    <!-- Kontainer untuk item keranjang belanja -->
    <div id="page-wrap">
      <!-- Judul untuk keranjang belanja -->
      <h1>Shopping Cart</h1>

      <!-- Melakukan loop untuk setiap item dalam cartItems dan membuat kontainer produk -->
      <ItemCart v-for="item in cartItems" :key="item.id" :item="item" />
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
import ItemCart from "@/components/ItemCart.vue";

export default {
  // Data yang digunakan dalam komponen ini
  components: { ItemCart },
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
</style>
