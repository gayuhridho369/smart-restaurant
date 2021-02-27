<template>
  <div class="foods">
    <navbar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h3><strong>Foods </strong> List</h3>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col-lg-6">
          <div class="input-group flex-nowrap">
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Search..."
              aria-label="Search"
              aria-describedby="addon-wrapping"
              @keyup="searchFood"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="addon-wrapping">
                <b-icon-search></b-icon-search>
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mb-4">
        <div
          class="col-md-3 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "foods",
  components: {
    Navbar,
    CardProduct,
  },

  data() {
    return {
      products: [],
      search: "",
    };
  },

  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchFood() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log(error));
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>