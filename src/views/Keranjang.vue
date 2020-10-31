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
              <td>{{pesan.keterangan ? pesan.keterangan : '-'}}</td>
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
              <td><strong>Rp. {{totalHarga ? totalHarga : '0'}} </strong></td>
            </tr>
          </tbody>
        </table>
      </div>
       </div>
     </div>

     <div class="row">
       <div class="col-md-6">

       </div>
       <div class="col-md-6">
         <form method="post" @submit.prevent="simpan">
            <div class="form-group">
              <label for="jumlah_pesanan">Nama</label>
              <input type="text" class="form-control" id="jumlah_pesanan" v-model="pesan.nama" autocomplete="off">
            </div>
            <div class="form-group">
              <label for="Keterangan">Nomer Meja</label>
              <input type="number" class="form-control" id="jumlah_pesanan" v-model="pesan.noMeja">
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

  name:'Keranjang',
  components:{
    Navbar,
 
    
  },

  data(){

    return {

      pesanan:[],
      pesan:{

        nama:'',
        noMeja:'',
        detail:[]
      },

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


    },

    async simpan(){

      if (this.pesan.nama && this.pesan.noMeja) {
      
        await axios.post('http://localhost:3000/pesanan',this.pesan,this.pesan.  detail=this.pesanan)

        this.pesanan.map(p => axios.delete('http://localhost:3000/keranjang/'+ p.id) )
        

        this.$toast.success('Berhasil Memesan',{
  
          type:'success',
          duration:3000,
          position:'top-right'
  
        })

      this.$router.push('/detail')
      
      }else{

         this.$toast.error('Isi Nama Dan No Meja',{
  
          type:'error',
          duration:3000,
          position:'top-right'
  
        })
      }



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