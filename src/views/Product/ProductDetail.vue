<template lang="">
  <div>
    <div id="page-wrap" v-if="product">
      <h4 v-if="notif" class="notif">Item Added Successfully!</h4>
      <div id="img-wrap">
        <img :src="`http://localhost:8000${product.imageUrl}`" alt="" />
      </div>
      <div id="product-details">
        <h1>{{ product.name }}</h1>
        <p>{{ product.description }}</p>
        <p id="price">Rp. {{ product.price }}</p>
        <p id="">Average Rating: {{ product.averageRating }}</p>
        <button @click="addToCart(product.code)" id="add-to-cart">Add to cart</button>
      </div>
    </div>
    <NotFound v-else />
  </div>
</template>
<script>
// Mengimpor data produk dari file data-seed yang ada di folder src
// import { products } from "@/data-seed";
import axios from "axios";
import NotFound from "../Errors/NotFound.vue";

export default {
  // Fungsi data yang mengembalikan objek yang berisi data untuk komponen ini
  components: {
    NotFound,
  },
  data() {
    return {
      // Menyimpan data produk yang diimpor dalam state komponen
      product: {},

      // products,
      notif: false,
      // NotFound,
    };
  },
  methods: {
    async addToCart(product) {
      if (this.isAddingToCart) return; // Jika sudah dalam proses, return
      this.isAddingToCart = true; // Set jadi true saat proses berlangsung
      await axios.post("http://localhost:8000/api/orders/user/1/add", {
        product: product,
      });
      this.notif = true;
      this.isAddingToCart = false; // Kembalikan ke false setelah proses selesai
    },
  },
  // computed = fungsi untuk mengubah suatu data yang sudah ada ke dalam format baru/ke dalam format yang kita inginkan
  // Bagian computed untuk mendefinisikan properti yang dihitung secara reaktif
  // computed: {
  //   // Properti computed untuk menemukan produk berdasarkan ID dari route
  //   product() {
  //     // Mencari produk dalam array 'products' yang ID-nya cocok dengan ID dari parameter route
  //     return this.products.find((product) => product.id === this.$route.params.id);
  //   },
  // },

  // Lifecycle hook yang dijalankan setelah komponen dipasang ke DOM
  // mounted() {
  //   // Mencetak produk yang ditemukan ke konsol untuk debugging
  //   console.log(this.product);
  //   // Kode berikut ini merupakan alternatif cara manual untuk menemukan produk
  //   // const id = this.$route.params.id;
  //   // this.product = products.find((product) => product.id === id);
  // },
  async created() {
    // Fungsi 'created' adalah lifecycle hook Vue.js yang dipanggil setelah instance Vue telah dibuat.
    // Kata kunci 'async' memungkinkan penggunaan 'await' di dalam fungsi ini untuk menangani operasi asinkron.

    const code = this.$route.params.id;
    // Mengambil parameter 'id' dari URL route saat ini dan menyimpannya dalam variabel 'code'.
    // 'this.$route' adalah objek yang menyediakan informasi tentang route saat ini,
    // dan 'params' berisi parameter dari route, seperti ID produk yang akan diambil.

    const result = await axios.get(`http://localhost:8000/api/products/${code}`);
    // Mengirim permintaan HTTP GET ke URL yang dibangun dengan base URL dan 'code' sebagai parameter ID produk.
    // 'await' menunggu hingga permintaan selesai dan mendapatkan hasil dari server.
    // 'axios.get' mengembalikan sebuah Promise yang akan diselesaikan dengan respons dari server.

    this.product = result.data;
    // Menyimpan data produk yang diterima dari server ke dalam variabel data 'product' di instance Vue.
    // 'result.data' adalah data yang diterima dari respons server, yang berisi informasi produk.
  },
};
</script>

<style scoped>
#page-wrap {
  margin-top: 16px;
  padding: 16px;
  max-width: 600px;
}

#img-wrap {
  text-align: center;
}

img {
  width: 400px;
}

#product-details {
  padding: 16px;
  position: relative;
}

#add-to-cart {
  width: 100%;
}

#price {
  position: absolute;
  top: 24px;
  right: 16px;
}

.notif {
  text-align: center;
  color: white;
  background-color: #41b883;
  padding: 3%;
  border-radius: 8px;
}
</style>
