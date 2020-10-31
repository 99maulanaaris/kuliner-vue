<template>
  

  <div class="FoodDetail ">
      <Navbar/>
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item "><router-link class="text-dark" :to="{name:'Home'}">Home</router-link></li>
              <li class="breadcrumb-item "><router-link class="text-dark" :to="{name:'Foods'}">Foods</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Detail Pesanan</li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-4">
        <div class="col-md-6">
          <img :src="`../assets/img/${pesanan.gambar}`" class="img-fluid shadow">  
        </div>
        <div class="col-md-6">
          <h2><strong>{{pesanan.nama}}</strong></h2>
          <hr>
          <h4>Harga :<strong> Rp.{{pesanan.harga}}</strong></h4>
          
          <form method="post" @submit.prevent="store">
            <div class="form-group">
              <label for="jumlah_pesanan">Jumlah Pesan</label>
              <input type="number" class="form-control" id="jumlah_pesanan" v-model="keranjang.jumlah" autocomplete="off">
            </div>
            <div class="form-group">
              <label for="Keterangan">Keterangan</label>
              <textarea v-model="keranjang.keterangan" id="keterangan" rows="5" class="form-control" placeholder="Keterangan Makanan"></textarea>
            </div>

            <button type="submit" class="btn" ><b-icon-cart-check></b-icon-cart-check> Pesan</button>
          </form>

        </div>
      </div>
    
    </div>
  </div>

</template>

<script>

import Navbar from '@/components/Navbar.vue'
import axios from 'axios'

export default {

  name: 'FoodDetail',

  components:{

    Navbar,
  },

  data(){

    return {

      pesanan: [],

      keranjang:{

        keterangan:'',
        
        jumlah:'',

        product:[]
      }
      

    }
  },

  mounted(){

    this.getDetails()
  },

  methods : {

    async getDetails(){

      let response = await axios.get('http://localhost:3000/product/'+this.$route.params.id)
      
      if (response.status === 200) {

        this.pesanan = response.data
      }

    },

    async store(){

      if (this.keranjang.jumlah) {
        
         await axios.post('http://localhost:3000/keranjang',this.keranjang,this.keranjang.product = this.pesanan)
          
          this.$toast.success('Berhasil Masuk Keranjang',{

          type:'success',
          duration:3000,
          position:'top-right',

        })

        
      

        this.$router.push({path:'/keranjang'})
      
      }else{
        
          this.$toast.error('Masukan Jumlah Pesanan',{
          type:'error',
          duration:3000,
          position:'top-right',

        })

      }

    },

  }

}
</script>
