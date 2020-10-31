<template>
  <div class="CardProduct">
      <div class="card shadow card-product">
        <img :src="`assets/img/`+ product.gambar" class="card-img-top">
        <div class="card-body">
          <h5 class="card-title">{{product.nama}}</h5>
          <p class="card-text">Harga : Rp.  {{product.harga}}</p>
          <router-link :to="{ name: 'FoodDetail', params:{id:product.id} }" class="btn"><b-icon-cart-check></b-icon-cart-check> Pesan</router-link>
        </div>
      </div>
  </div>
</template>

<script>
export default {

    name: "CardProduct",
    props: ['product'],

}
</script>
