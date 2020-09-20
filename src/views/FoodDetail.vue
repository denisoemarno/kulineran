<template>
  <div class="FoodDetail">
    <Navbar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-secondary">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">Food Order</li>
            </ol>
          </nav>
        </div>
      </div>
      <!-- end breadcrumb -->
      <div class="row mb-3">
        <div class="col-md-6 m-auto">
          <img :src="'../assets/images/' + product.gambar" class="img-fluid shadow" />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            <strong>Harga : Rp. {{ product.harga }}</strong>
          </h4>
          <br />
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan">Jumlah Pesan</label>
              <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan" />
            </div>
            <div class="form-group">
              <label for="Keterangan">Keterangan</label>
              <textarea
                v-model="pesan.keterangan"
                class="form-control"
                placeholder="Keterangan Seperti: Pedas , Nasinya Setengah"
              ></textarea>
              <hr />
              <button class="btn btn-success col-md-12" type="submit" @click="pemesanan">
                <b-icon-cart></b-icon-cart>Pesan
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push ({ path: "/keranjang" })
            this.$toast.success("Sukses Masuk Keranjang", {
              type: "success",
              position: "top",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      }else {
        this.$toast.error("Jumlah Pesanan Harus Diisi", {
              type: "error",
              position: "top",
              duration: "3000",
              dismissible: true,
            });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      // handle success

      .catch((error) => console.log("Gagal :", error));
    // handle error
  },
};
</script>

<style>
</style>