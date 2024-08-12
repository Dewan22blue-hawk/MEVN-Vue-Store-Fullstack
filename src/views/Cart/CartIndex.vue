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
// import { cartItems } from "@/data-seed";
import axios from "axios";
import ItemCart from "@/components/ItemCart.vue";

export default {
  // Data yang digunakan dalam komponen ini
  components: { ItemCart },
  data() {
    return {
      // cartItems berisi array item yang ada di keranjang
      // cartItems,
      cartItems: [],
    };
  },
  // Bagian computed untuk menghitung total harga
  computed: {
    totalPrice() {
      // Menghitung total harga dengan menjumlahkan harga setiap item di cartItems
      return this.cartItems.reduce((sumCart, item) => sumCart + Number(item.price), 0).toFixed(2);
    },
  },
  // Fungsi yang dipanggil ketika komponen ini dijalankan
  async created() {
    // Mengambil data cartItems dari server menggunakan axios
    const result = await axios.get("http://localhost:8000/api/orders/user/1");
    // Menunggu respons dari server dan menyimpan hasilnya dalam variabel `result`

    // karena response nya array maka kita lakukan object assign
    let data = Object.assign(
      {},
      ...result.data.map((result) => ({
        cart_items: result.products,
      }))
    );
    // Mengubah data dari array ke objek dengan properti `cart_items` berisi produk
    // Ini mungkin perlu jika format data dari server tidak langsung sesuai

    // this.cartItems = result.data;
    this.cartItems = data.cart_items;
    // Mengupdate `cartItems` di komponen dengan data produk yang diperoleh
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
