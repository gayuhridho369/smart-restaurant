<template>
  <div class="pesanan-sukses">
    <Navbar />
    <div class="container">
      <div class="row justify-content-cente mt-5">
        <div class="col text-center">
          <h2>
            <strong>Ordering Success</strong>
          </h2>
          <img src="../assets/images/waiting.png" width="300" />
          <h4>Please wait for a minutes...</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
export default {
  name: "OrderSuccess",
  components: { Navbar },
};
</script>

<style>
</style>