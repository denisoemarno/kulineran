<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <a class="navbar-brand" href="#">
          <img
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcS1Cv63eNSg6ic9UTcwTYBNUTlF2vqezdNLWg&usqp=CAU"
            width="150"
            height="100"
            class="d-inline-block align-top"
            alt
            loading="lazy"
          />
        </a>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <router-link class="nav-link" to="/">Home</router-link>
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-form>
              <router-link class="nav-link" to="/keranjang">
                Keranjang
                <b-icon-bag></b-icon-bag>
                <span
                  class="badge badge-success ml-2"
                >{{ updateKeranjang ? updateKeranjang.length: jumlah_pemesanans.length }}</span>
              </router-link>
            </b-nav-form>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Navbar",
  data() {
    return {
      jumlah_pemesanans: [],
    };
  },
  props: ["updateKeranjang"],
  methods: {
    setJumlah(data) {
      this.jumlah_pemesanans = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setJumlah(response.data))
      // handle success

      .catch((error) => console.log("Gagal :", error));
    // handle error
  },
};
</script>

<style>
</style>