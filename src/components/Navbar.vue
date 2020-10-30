<template>
  <nav class="navbar navbar-expand-lg navbar-light">
  <div class="container">
      <a class="navbar-brand" href="#">KULINERIA</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
    
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item ">
            <router-link class="nav-link" exact to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">Foods</router-link>
          </li>
        </ul>

        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" exact to="/Keranjang">
            Keranjang
            <b-icon-bag></b-icon-bag>
            <span class="badge badge-success ml-2">{{update ?update.length:jumlah.length}}</span>
            </router-link>
          </li>
        </ul>
      </div>
  </div>
</nav>
</template>

<script>

import axios from 'axios'
export default {

    name : 'Navbar',

    props:['update'],

    data(){
      
      return{

        jumlah:[],

      }
    },

    mounted(){

      this.getJumlah()

    },

    methods:{

      async getJumlah(){

        let response = await axios.get('http://localhost:3000/keranjang')

        if (response.status === 200) {
          
          this.jumlah = response.data

        }

      }


    }


    

}
</script>

<style>

</style>