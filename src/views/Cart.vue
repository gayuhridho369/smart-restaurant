<template>
  <div class="cart">
    <Navbar :updateCart="cart" />
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
                Food Cart
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Food <strong>Cart</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Image</th>
                  <th scope="col">Food Name</th>
                  <th scope="col">Note</th>
                  <th scope="col">Quantity</th>
                  <th scope="col">Price</th>
                  <th scope="col">Total</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(cart, index) in cart" :key="cart.id">
                  <th scope="row">{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/images/' + cart.product.image"
                      class="img-fluid shadow"
                      width="200"
                    />
                  </td>
                  <td>
                    <strong>{{ cart.product.name }}</strong>
                  </td>
                  <td>{{ cart.note ? cart.note : "-" }}</td>
                  <td>{{ cart.quantity }}</td>
                  <td>Rp. {{ cart.product.price }}</td>
                  <td>
                    <strong>
                      Rp. {{ cart.product.price * cart.quantity }}</strong
                    >
                  </td>
                  <td class="text-danger" align="center">
                    <b-icon-trash
                      @click="deleteItemCart(cart.id)"
                    ></b-icon-trash>
                  </td>
                </tr>

                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Price : </strong>
                  </td>
                  <td>
                    <strong>Rp. {{ totalPrice }}</strong>
                  </td>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- Form Checkout -->

      <div class="row justify-content-end">
        <div class="col-md-4">
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="name"> <h5>Name</h5></label>
              <input type="text" class="form-control" v-model="order.name" />
            </div>

            <div class="form-group">
              <label for="tableNumber"> <h5>Table number</h5></label>
              <input
                type="number"
                class="form-control"
                v-model="order.tableNumber"
              />
            </div>

            <button type="submit" class="btn btn-success" @click="checkout">
              <b-icon-cart-check> </b-icon-cart-check> Order
            </button>
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
  name: "Cart",
  components: {
    Navbar,
  },

  data() {
    return {
      cart: [],
      order: {},
    };
  },

  methods: {
    setCart(data) {
      this.cart = data;
    },
    deleteItemCart(id) {
      axios
        .delete("http://localhost:3000/cart/" + id)
        .then(() => {
          this.$toast.success("Delete Item Success", {
            type: "success",
            position: "top",
            duration: 3000,
            dismissible: true,
          });

          // Update data cart
          axios
            .get("http://localhost:3000/cart")
            .then((response) => this.setCart(response.data))
            .catch((error) => console.log(error));
        })
        .catch((error) => console.log(error));
    },
    checkout() {
      if (this.order.name && this.order.tableNumber) {
        this.order.cart = this.cart;

        axios
          .post("http://localhost:3000/order", this.order)
          .then(() => {
            // Delete All Cart
            this.cart.map(function (item) {
              return axios
                .delete("http://localhost:3000/cart/" + item.id)
                .catch((error) => console.log(error));
            });

            this.$router.push({ path: "/order-success" });
            this.$toast.success("Order Success", {
              type: "success",
              position: "top",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((error) => console.log(error));
      } else {
        this.$toast.error("Name and Table Number is required", {
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
      .get("http://localhost:3000/cart")
      .then((response) => this.setCart(response.data))
      .catch((error) => console.log(error));
  },

  computed: {
    totalPrice() {
      return this.cart.reduce(function (items, data) {
        return items + data.product.price * data.quantity;
      }, 0);
    },
  },
};
</script>

<style>
</style>