<template>
  <!-- v-for="product in products" :key="product.id" -->
  <div class="product-item">
    <!-- :src: Binding directive di Vue.js yang mengikat atribut src dari elemen <img>.
`http://localhost:8000${product.imageUrl}`: Template literal (backticks) digunakan untuk menyusun string URL gambar. product.imageUrl adalah property yang menyimpan URL gambar relatif dari produk.
http://localhost:8000: Base URL server tempat gambar disimpan. Menggabungkannya dengan product.imageUrl membentuk URL lengkap ke gambar. -->
    <img :src="`http://localhost:8000${product.imageUrl}`" alt="" />
    <h3 class="product-name">{{ product.name }}</h3>
    <p class="product-price">{{ product.price }}</p>
    <router-link :to="{ name: 'productDetail', params: { id: product.id } }">
      <button>Detail</button>
    </router-link>
  </div>
</template>

<script>
export default {
  props: ["product"],
};
</script>

<style scoped>
.product-item {
  align-items: center;
  border-radius: 8px;
  box-shadow: 0px 2px 5px #888;
  display: flex;
  flex-direction: column;
  margin-bottom: 2%;
  padding: 20px;
  position: relative;
  width: 32%;
}

.product-name {
  margin-bottom: 0;
}

img {
  height: 200px;
  width: 200px;
  border-radius: 5%;
}

a {
  width: 100%;
}

button {
  width: 100%;
}
</style>
