<template>
    <div class="">
        <Navbar />
        <div class="container">
            <div class="row mt-4">
                <div class="col">
                    <h2>Daftar <strong>Makanan</strong></h2>
                </div>
            </div>
            <div class="row mt-3">
                <div class="col">
                    <div class="input-group mb-3">
                        <input v-model="search" @keyup="searchFood" type="text" class="form-control" placeholder="Mau makan apa hari ini ?" aria-label="Cari"
                            aria-describedby="basic-addon1">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="basic-addon1">
                            <b-icon-search />
                            </span>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row mt-5 mb-4">
                <div class="col-md-4 mb-3" v-for="product in products" :key="product.id">
                    <Card :product="product" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/NavbarComponent.vue'
import Card from '@/components/CardComponent.vue'
import axios from 'axios'
import {API} from '@/router/api.js'

export default {
    name: "FoodsView",
    components: {
        Navbar,
        Card

    },
    data() {
        return {
            products: [],
            search: ""
        }
    },
    methods: {
        setProduct(data) {
            this.products = data
        },
        searchFood(){
            axios
            .get(API+'/products?q='+this.search)
            .then((response) =>
                // handle success
                this.setProduct(response.data)
            )
            .catch(function (error) {
                // handle error
                console.log(error);
            })
        }
    },
    mounted() {
        axios
            .get(API+'/products')
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

<style>
</style>