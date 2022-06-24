<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h2>Best <strong> Foods</strong></h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-sm btn-success float-right">
            <b-icon-eye /> Lihat Semua
          </router-link>
        </div>
      </div>
      <div class="row mt-5 mb-4">
        <div class="col-md-4 mb-3" v-for="product in products" :key="product.id">
          <Card :product="product"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/NavbarComponent.vue'
import Hero from '@/components/HeroComponent.vue'
import Card from '@/components/CardComponent.vue'
import {API} from '@/router/api.js'
import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    Navbar,
    Hero,
    Card
  },
  data() {
    return {
      products: []
    }
  },
  methods: {
    setProduct(data) {
      this.products = data
    }
  },
  mounted(){
    axios
      .get(API+'/best-products')
      .then((response) =>
        // handle success
        this.setProduct(response.data)
      )
      .catch(function (error) {
        // handle error
        console.log(error);
      })
  }
}
</script>
