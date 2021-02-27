<template>
  <div class="banner">
    <!-- Desktop -->
    <div class="d-none d-md-block">
      <div class="row mt-3">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Smart Restaurant</strong> <br />
                Our Menu on Your Gadget
              </h2>
              <p>Let's choose and order your favourite food</p>

              <router-link class="btn btn-success" to="foods">
                Order
                <b-icon-arrow-bar-right></b-icon-arrow-bar-right>
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/images/banner-draw.png" width="100%" />
        </div>
      </div>
    </div>

    <!-- Mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-3">
        <div class="col-md-6">
          <img src="../assets/images/banner-draw.png" width="100%" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Smart Restaurant</strong> <br />
                Our Menu on Your Gadget
              </h2>
              <p>Let's choose and order your favourite food</p>

              <button class="btn btn-success">
                Order
                <b-icon-arrow-bar-right></b-icon-arrow-bar-right>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style>
</style>