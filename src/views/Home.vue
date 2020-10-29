<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />


      <div class="row mt-4">
        <div class="col">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col">
          <router-link :to="{name:'Foods'}" class="btn btn-success float-right"><b-icon-eye></b-icon-eye> Lihat Semua</router-link>
        </div>
      </div>

      <div class="row mb-4">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
          <CardProduct :product='product'/>
        </div>
      </div>


    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct.vue'
import axios from 'axios'

export default {
  name: 'Home',

  components: {
    Navbar,
    Hero,
    CardProduct
  },

  data()
  {
    return {
       
       products: []
      
    }
  },
  
  mounted()
  {
    this.getProduct()
  },

  methods : {

    async getProduct(){

      let response = await axios.get('http://localhost:3000/best-product')

      if (response.status === 200) {
        
        this.products = response.data
      }
    }

  }

  


}
</script>
