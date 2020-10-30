<template>
  <div class="Keranjang">
    <Navbar :update="pesanan"/>
    <div class="container">
     <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item "><router-link class="text-dark" :to="{name:'Home'}">Home</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Keranjang</li>
            </ol>
          </nav>
        </div>
     </div>
    
      <h3>Detail <strong>Pesanan</strong></h3>
     <div class="row mt-3">
       <div class="col">
         <div class="table-responsive">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">No</th>
              <th scope="col">Gambar</th>
              <th scope="col">Nama Makanan</th>
              <th scope="col">Keterangan</th>
              <th scope="col">Jumlah</th>
              <th scope="col">Harga</th>
              <th scope="col">Total Harga</th>
              <th scope="col">Aksi</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(pesan,index) in pesanan" :key="pesan.id">
              <th scope="row">{{index+1}}</th>
              <td>
                <img :src="`../assets/img/${pesan.product.gambar}`" class="img-fluid" width="200px">
              </td>
              <td>{{pesan.product.nama}}</td>
              <td>{{pesan.keterangan ? pesan.keteranagan : '-'}}</td>
              <td>{{pesan.jumlah}}</td>
              <td>{{pesan.product.harga}}</td>
              <td>
                Rp. {{pesan.product.harga * pesan.jumlah}}
              </td>
              <td>
                <button type="submit" class="text-danger tombol" @click="hapusData(pesan.id)"><b-icon-trash></b-icon-trash></button>
              </td>
            </tr>
            <tr>
              <td colspan="6" align="right"><strong>Total Bayar : </strong></td>
              <td><strong>Rp. {{totalHarga}} </strong></td>
            </tr>
          </tbody>

        </table>
      </div>
       </div>
     </div>
      
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import axios from 'axios'

export default {

  name:'Keranjang',
  components:{
    Navbar,
 
    
  },

  data(){

    return {

      pesanan:[],
      product:[],
    }
    
  },

  mounted(){

    this.getPesanan()

  },

  methods:{

    async getPesanan(){

      let response = await axios.get('http://localhost:3000/keranjang')
      if (response.status === 200) {
        
        this.pesanan = response.data

      }

    },

    async hapusData(id){

       await axios.delete('http://localhost:3000/keranjang/'+id)

       this.$toast.success('Berhasil Dihapus',{

         type:'error',
         duration:3000,
         position:'top-right'

       })

       let response = await axios.get('http://localhost:3000/keranjang')
       this.pesanan = response.data


    }

  },

  computed:{
    
    totalHarga(){

      return this.pesanan.reduce(function (harga1,harga2) {
        
        return harga1 + (harga2.product.harga * harga2.jumlah)

      },0)
    }

  }


}
</script>

<style>

</style>