<template>
  <div class="food-detail">
    <navbar />
    <div class="container">
      <!-- Breadcrumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Detail
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <!-- Food Detail -->
      <div class="row mt-2">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.image"
            class="img-fluid shadow"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.name }}</strong>
            <hr />
            <h4>
              Price : <strong>Rp. {{ product.price }}</strong>
            </h4>
            <form v-on:submit.prevent>
              <div class="form-group">
                <label for="quantity"> <h5>Quantity</h5></label>
                <input
                  type="number"
                  class="form-control"
                  v-model="order.quantity"
                />
              </div>
              <div class="form-group">
                <label for="note"> <h5>Note</h5></label>
                <textarea
                  v-model="order.note"
                  id="note"
                  class="form-control"
                  placeholder="..."
                ></textarea>
              </div>

              <button type="submit" class="btn btn-success" @click="addToCart">
                <b-icon-cart-plus> </b-icon-cart-plus> Add to Cart
              </button>
            </form>
          </h2>
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
      order: {},
    };
  },

  methods: {
    setProduct(data) {
      this.product = data;
    },
    addToCart() {
      if (this.order.quantity) {
        this.order.product = this.product;
        axios
          .post("http://localhost:3000/cart", this.order)
          .then(() => {
            this.$router.push({ path: "/cart" });
            this.$toast.success("Add to Cart Success", {
              type: "success",
              position: "top",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Quantity is required", {
          type: "error",
          position: "top",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>