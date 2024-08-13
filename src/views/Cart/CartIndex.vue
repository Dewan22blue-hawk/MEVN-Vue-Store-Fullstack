<template lang="">
  <!-- Elemen utama pembungkus -->
  <div>
    <!-- Kontainer untuk item keranjang belanja -->
    <div id="page-wrap">
      <!-- Judul untuk keranjang belanja -->
      <h1>Shopping Cart</h1>

      <!-- Melakukan loop untuk setiap item dalam cartItems dan membuat kontainer produk -->
      <!-- $event ini akan menangkap nilai dari parameter kedua yang ada didalam emit pada case ini adalah item.code -->
      <ItemCart v-for="item in cartItems" :key="item.id" :item="item" v-on:remove-item="removeFromCart($event)" />
      <!-- v-on:remove-item: Ini mendengarkan event custom bernama 'remove-item' yang dipancarkan (emit) dari dalam komponen child ItemCart.
removeFromCart($event): Ketika event 'remove-item' dipancarkan dari komponen ItemCart, methode removeFromCart akan dipanggil jadi kita buat methodsnya di script. ($event) adalah data yang dipancarkan bersama event, dalam hal ini biasanya berupa item.code atau identifikasi item lainnya yang ingin dihapus. -->
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
  methods: {
    // Metode removeFromCart yang dijalankan secara asinkron
    async removeFromCart(product) {
      // Mengirim permintaan HTTP DELETE ke server untuk menghapus item dari keranjang belanja berdasarkan produk yang diberikan
      await axios
        .delete(`http://localhost:8000/api/orders/user/1/product/${product}`)
        // Jika terjadi kesalahan, menangkapnya dan mencetak pesan kesalahan ke konsol
        .catch((err) => console.log(err));

      // Mencari indeks item yang akan dihapus dari cartItems berdasarkan kode produk
      let indexCart = this.cartItems
        // Mendeklarasikan variabel indexCart yang akan digunakan untuk menyimpan indeks dari item yang akan dihapus dalam array cartItems.
        // Menggunakan metode map pada cartItems untuk membuat array baru yang hanya berisi kode produk (item.code) dari setiap item dalam keranjang.
        .map(function (item) {
          return item.code;
        })
        // Menggunakan indexOf untuk menemukan indeks dari produk dalam array kode produk yang sesuai dengan parameter product. Indeks ini menunjukkan posisi item dalam array cartItems yang ingin dihapus.
        .indexOf(product);

      // Menghapus item dari array cartItems di posisi yang ditemukan
      // Menggunakan metode splice untuk menghapus satu item dari array cartItems pada posisi indexCart, yaitu item yang memiliki kode produk yang sesuai dengan yang ingin dihapus.
      this.cartItems.splice(indexCart, 1);
    },
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
