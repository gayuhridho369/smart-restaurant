<template>
  <div class="card shadow card-product">
    <img
      :src="'assets/images/' + product.image"
      class="card-img-top"
      alt="..."
    />
    <div class="card-body">
      <h5 class="card-title">{{ product.name }}</h5>
      <p class="card-text">Harga : Rp. {{ product.price }}</p>
      <router-link :to="'/food/' + product.id" class="btn btn-success">
        <b-icon-cart></b-icon-cart> Order
      </router-link>
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