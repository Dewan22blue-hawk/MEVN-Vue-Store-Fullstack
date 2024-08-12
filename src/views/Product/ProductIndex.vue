<template>
  <div>
    <div id="page-wrap">
      <div class="grid-wrap">
        <!-- jika memanfaatkan index dari perulangan -->
        <!-- <div v-for="(product,index) in products" :key="product.id" class="product-item"> -->
        <ProductItem v-for="product in products" :key="product.id" :product="product" />
      </div>
    </div>
  </div>
</template>
<script>
// import variabel product yang ada didalam file data-seed.js
// import { products } from "@/data-seed";
// import diatas adalah Tilase nganggo seed.js
// Mengimpor modul `axios` untuk melakukan permintaan HTTP.
import axios from "axios";
// Mengimpor komponen `ProductItem` dari path relatif ke komponen Vue.js.
import ProductItem from "../../components/ProductItem.vue";

export default {
  components: {
    // Mendaftarkan komponen `ProductItem` yang akan digunakan di dalam template komponen ini.
    ProductItem,
  },
  data() {
    return {
      // Mendefinisikan variabel `products` yang akan digunakan untuk menyimpan data produk.
      // `products` diinisialisasi sebagai array kosong.
      products: [],
    };
  },
  async created() {
    // `created` adalah lifecycle hook yang dipanggil setelah komponen diinstansiasi.
    // Menggunakan `async` untuk menangani operasi asinkron dengan `await`.

    const result = await axios.get("http://localhost:8000/api/products");
    // Mengirimkan permintaan GET ke URL API untuk mendapatkan data produk.
    // Menyimpan hasil data dari API ke dalam variabel `result`.

    this.products = result.data;
    // Menetapkan data produk yang diterima dari API ke properti `products` di data komponen.
    // Ini akan memicu pembaruan tampilan dengan data produk baru.

    // console.log(result.data);
    // (Komentar) Menampilkan data hasil dari API di konsol untuk keperluan debugging (opsional).
  },
};
</script>

<!-- scoped artinya style ini hanya bisa digunakan pada komponen index ini dan jika ada komponen yang kita panggil didalam index tersebut maka styling nya akan tidak bekerja -->
<style scoped>
.grid-wrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 16px;
}
</style>
