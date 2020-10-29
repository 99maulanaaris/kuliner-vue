<template>
    <div class="Foods">
        <Navbar />
        <div class="container">
          <div class="row mt-4">
            <div class="col">
              <h2>Daftar Makanan</h2>
            </div>
          </div>

          <div class="row mt-3">
            
            <div class="col">
              <div class="input-group mb-3">
              <input v-model="search" @keyup="searchFoods" type="text" class="form-control" placeholder="Cari Makananmu" aria-label="Cari" aria-describedby="basic-addon1">

              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">
                  <b-icon-search></b-icon-search>
                </span>
              </div>
            </div>
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
import CardProduct from '@/components/CardProduct.vue'
import axios from 'axios'

export default {
  name: 'Foods',
  components: {
    Navbar,
    CardProduct,
  },

   data()
  {
    return {
       
       products: [],

       search: '',
      
    }
  },
  
  mounted()
  {
    this.getProduct(),

    this.searchFoods()
  },

  methods : {

    async getProduct(){

      let response = await axios.get('http://localhost:3000/product')

      if (response.status === 200) {
        
        this.products = response.data
      }
    },

    async searchFoods(){
      
      let response = await axios.get('http://localhost:3000/product?q='+ this.search)

      if (response.status === 200) {
        
        this.products = response.data
      }

    }

  }
}
</script>