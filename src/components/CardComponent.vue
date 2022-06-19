<template>
<div class="card shadow card-product">
  <img :src="`assets/images/`+product.gambar" class="card-img-top" alt="">
  <div class="card-body">
    <h5 class="card-title">{{product.nama}}</h5>
    <p class="card-text">Rp. {{ product.harga }} </p>
    <router-link :to="'/food/'+product.id" class="btn btn-success btn-sm"> <b-icon-cart /> Pesan</router-link>
  </div>
</div>
</template>

<script>
export default {    
    name: 'CardComponent',
    props: ['product']
}
</script>

<style>

</style>