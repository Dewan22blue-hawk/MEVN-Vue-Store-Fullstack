<template>
  <div>
    <h1>Product Page</h1>
  </div>
</template>
<script>
export default {};
</script>

<!-- scoped artinya style ini hanya bisa digunakan pada komponen index ini dan jika ada komponen yang kita panggil didalam index tersebut maka styling nya akan tidak bekerja -->
<style scoped>
.grid-wrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 16px;
}

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
