<template>
  <div class="card shadow card-product">
    <img :src="'../assets/images/' + product.gambar" class="card-img-top" alt="..." />
    <div class="card-body">
      <h5 class="card-title">
        <strong>{{product.nama}}</strong>
      </h5>
      <p class="card-text">
          Harga : Rp. {{product.harga}}
      </p>
      <router-link class="btn btn-success" :to="'/foods/'+product.id"><b-icon-cart></b-icon-cart>Pesan</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script>

<style>
</style>