<template>
    <div class="food-detail">
        <Navbar />
        <div class="container">
            <div class="row mt-5">
                <div class="col">
                    <nav aria-label="breadcrumb">
                        <ol class="breadcrumb">
                            <li class="breadcrumb-item">
                                <router-link to="/">Home</router-link>
                            </li>
                            <li class="breadcrumb-item" aria-current="page">
                                <router-link to="/foods">Foods</router-link>
                            </li>
                            <li class="breadcrumb-item active" aria-current="page">Food Details</li>
                        </ol>
                    </nav>
                </div>
            </div>
            <div class="row mt-4">
                <div class="col-md-6">
                    <img :src="`../assets/images/` + product.gambar" width="100%" class="shadow img-fluid" />
                </div>
                <div class="col-md-6 mt-3 mt-md-0 mt-lg-0">
                    <h2><strong>{{ product.nama }}</strong></h2>
                    <hr>
                    <h4>Harga : <strong>Rp. {{ product.harga }} </strong> </h4>
                    <form v-on:submit.prevent>
                        <div class="form-group">
                            <label for="Jumlah_pesanan">Jumlah Pesan</label>
                            <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan">
                        </div>
                        <div class="form-group">
                            <label for="keterangan">Keterangan</label>
                            <textarea class="form-control" placeholder="Keterangan "
                                v-model="pesan.keterangan"></textarea>
                        </div>
                        <button @click="pemesanan" type="submit" class="btn btn-success btn-sm">
                            <b-icon-cart /> Pesan
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/NavbarComponent.vue'
import axios from 'axios'
import { API } from '@/router/api'

export default {
    name: 'FoodDetailView',
    components: {
        Navbar,
    },
    data() {
        return {
            product: {},
            pesan: {}
        }
    },
    methods: {
        setProduct(data) {
            this.product = data
        },
        pemesanan() {
            if(this.pesan.jumlah_pemesanan ){
                this.pesan.product = this.product
                axios.post(API+"/keranjangs", this.pesan)
                .then(() => {
                    this.$router.push({path: "/keranjang"})
                    this.$toast.success('Sukses masuk kerajang.', {
                        // optional options Object
                        type:'success',
                        position: 'top-right',
                        duration: 3000,
                        dismissible:true
                        
                    })
                })
                .catch((err) => {
                    console.log(err)
                })
            }else {
                this.$toast.error('Jumlah pesanan harus diisi.', {
                        // optional options Object
                        type:'error',
                        position: 'top-right',
                        duration: 3000,
                        dismissible:true
                        
                    })
            }
                
        }
    },
    mounted() {
        axios
            .get(API+'/products/' + this.$route.params.id)
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