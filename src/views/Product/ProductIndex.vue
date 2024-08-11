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
import { products } from "@/data-seed";
import ProductItem from "../../components/ProductItem.vue";
export default {
  components: {
    ProductItem,
  },
  data() {
    return {
      products,
      // products: products,
    };
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
