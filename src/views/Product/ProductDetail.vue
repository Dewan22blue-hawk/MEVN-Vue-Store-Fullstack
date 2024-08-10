<template lang="">
  <div>
    <div id="page-wrap">
      <div id="img-wrap">
        <img :src="product.imageUrl" alt="" />
      </div>
      <div id="product-details">
        <h1>{{ product.name }}</h1>
        <p>{{ product.description }}</p>
        <p id="price">{{ product.price }}</p>
        <p id="">{{ product.averageRating }}</p>
        <button id="add-to-cart">Add to cart</button>
      </div>
    </div>
  </div>
</template>
<script>
// Mengimpor data produk dari file data-seed yang ada di folder src
import { products } from "@/data-seed";

export default {
  // Fungsi data yang mengembalikan objek yang berisi data untuk komponen ini
  data() {
    return {
      // Menyimpan data produk yang diimpor dalam state komponen
      products,
    };
  },
  // computed = fungsi untuk mengubah suatu data yang sudah ada ke dalam format baru/ke dalam format yang kita inginkan
  // Bagian computed untuk mendefinisikan properti yang dihitung secara reaktif
  computed: {
    // Properti computed untuk menemukan produk berdasarkan ID dari route
    product() {
      // Mencari produk dalam array 'products' yang ID-nya cocok dengan ID dari parameter route
      return this.products.find((product) => product.id === this.$route.params.id);
    },
  },

  // Lifecycle hook yang dijalankan setelah komponen dipasang ke DOM
  mounted() {
    // Mencetak produk yang ditemukan ke konsol untuk debugging
    console.log(this.product);
    // Kode berikut ini merupakan alternatif cara manual untuk menemukan produk
    // const id = this.$route.params.id;
    // this.product = products.find((product) => product.id === id);
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
</style>
