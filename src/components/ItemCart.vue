<template>
  <div class="product-container">
    <!-- Menampilkan gambar produk -->
    <img class="product-image" :src="`http://localhost:8000${item.imageUrl}`" alt="" />

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
</template>

<script>
export default {
  props: ["item"],
};
</script>

<style scoped>
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
