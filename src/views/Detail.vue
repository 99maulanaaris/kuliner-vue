<template>
  
  <div class="Detail">
      <Navbar/>
    <div class="container">
      
      <div class="row justify-content-center">
        <div class="col text-center">
          
        <img :src="`../assets/img/chef.png`" class="img-fluid" width="500px">
        
        <h2><strong>Yeayyy!!!!</strong></h2>
        
        <h3>Pesanan Kamu Sedang Di Proses</h3>
        </div>
      </div>


    </div>

  </div>


</template>

<script>

import Navbar from '@/components/Navbar.vue'

export default {

  name:'Detail',

  components:{

    Navbar,
  }
    
  

}
</script>

<style>

</style>