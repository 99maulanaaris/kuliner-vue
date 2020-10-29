<template>

<div class="hero">
    
  <!-- Desktop -->
  <div class="d-none d-md-block">
    <div class="row mt-4">
      <div class="col-md-6">
        <div class="d-flex h-100">
          <div class="justify-content-center align-self-center">
            <h2>
              <strong>Delicious</strong> Food Menu <br />
              in your gadget
            </h2>
            <p>
              Harga Murah Enak Dan Berkualitas , <strong>PESAN SEKARANG</strong>
            </p>
            <router-link to="/foods">
            <button class="btn btn-lg btn-success">  
              <b-icon-arrow-bar-right></b-icon-arrow-bar-right>
              Klik Disini
            </button>
            </router-link>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <img src="../assets/img/banner.png" width="100%" />
      </div>
    </div>
  </div>

  
  <!-- Mobile -->
  <div class="d-md-none d-sm-block">
    <div class="row mt-4">
      <div class="col-md-6">
        <img src="../assets/img/banner.png" width="100%" />
      </div>
      <div class="col-md-6 mt-4">
        <div class="d-flex h-100">
          <div class="justify-content-center align-self-center">
            <h2>
              <strong>Delicious</strong> Food Menu <br />
              in your gadget
            </h2>
            <p>
              Harga Murah Enak Dan Berkualitas , <strong>PESAN SEKARANG</strong>
            </p>
            <button class="btn btn-lg btn-success">
              <b-icon-arrow-bar-right></b-icon-arrow-bar-right>
              Klik Disini
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
  name: "Hero",
};
</script>
