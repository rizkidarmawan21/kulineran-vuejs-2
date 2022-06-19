<template>
    <div>
        <Navbar :updateKeranjang="keranjangs" />
        <div class="container">
            <div class="row mt-5">
                <div class="col">
                    <nav aria-label="breadcrumb">
                        <ol class="breadcrumb">
                            <li class="breadcrumb-item">
                                <router-link to="/">Home</router-link>
                            </li>
                            <li class="breadcrumb-item active" aria-current="page">Keranjang</li>
                        </ol>
                    </nav>
                </div>
            </div>

            <div class="row">
                <div class="col">
                    <h2>Keranjang <strong>Saya</strong> </h2>
                    <div class="mt-3" style="overflow-x:scroll">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th scope="col">#</th>
                                    <th scope="col">Foto</th>
                                    <th scope="col">Makanan</th>
                                    <th scope="col">Keterangan</th>
                                    <th scope="col">Jumlah</th>
                                    <th scope="col">Harga</th>
                                    <th scope="col">Total Harga</th>
                                    <th scope="col">Aksi</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                                    <th scope="row"> {{ 1 + index }} </th>
                                    <td> <img :src="`../assets/images/` + keranjang.product.gambar" width="120" alt="">
                                    </td>
                                    <td> {{ keranjang.product.nama }} </td>
                                    <td> {{ keranjang.keterangan ? keranjang.keterangan : '-' }} </td>
                                    <td> {{ keranjang.jumlah_pemesanan }} </td>
                                    <td> {{ keranjang.product.harga }} </td>
                                    <td>Rp. {{ (keranjang.product.harga * keranjang.jumlah_pemesanan) }} </td>
                                    <td align="center" class="text-danger">
                                        <b-icon-trash style="cursor:pointer" @click="hapusKeranjang(keranjang.id)" />
                                    </td>
                                </tr>
                                <tr>
                                    <td colspan="6" align="right"><strong>Total Harga:</strong></td>
                                    <td>Rp. {{ totalHarga }} </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>

            <div class="row justify-content-end">
                <div class="col-md-4">
                   <form v-on:submit.prevent>
                        <div class="form-group">
                            <label for="nama">Nama</label>
                            <input type="text" id="nama" class="form-control" v-model="pesan.nama" >
                        </div>
                        <div class="form-group">
                            <label for="noMeja">Nomor Meja</label>
                            <input type="text" id="noMeja" class="form-control" v-model="pesan.noMeja">
                        </div>
                        <button @click="checkout" type="submit" class="btn btn-success btn-sm float-right">
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
export default {
    name: 'KeranjangView',
    components: {
        Navbar,
    },
    data() {
        return {
            keranjangs: [],
            pesan: {}
        }
    },
    methods: {
        setKeranjang(data) {
            this.keranjangs = data
        },
        hapusKeranjang(id) {

            if (confirm('Yakin ingin menghapus pesanan ini ?')) {


                axios
                    .delete('http://localhost:3000/keranjangs/' + id)
                    .then(() =>
                        axios
                            .get('http://localhost:3000/keranjangs')
                            .then((response) =>
                                // handle success
                                this.setKeranjang(response.data)
                            )
                            .catch(function (error) {
                                // handle error
                                console.log(error);
                            }),

                        this.$toast.success('Sukses hapus kerajang.', {
                            // optional options Object
                            type: 'success',
                            position: 'top-right',
                            duration: 3000,
                            dismissible: true

                        })

                    )
                    .catch(function (error) {
                        this.$toast.error('Gagal menghapus keranjang.', {
                            // optional options Object
                            type: 'error',
                            position: 'top-right',
                            duration: 3000,
                            dismissible: true

                        })
                        console.log(error);
                    })

            }


        },
        checkout(){
            if(this.pesan.nama && this.pesan.noMeja){
                this.pesan.keranjang = this.keranjangs;
                axios.post("http://localhost:3000/pesanans", this.pesan)
                .then(() => {

                    this.keranjangs.map((item) => {
                        axios
                    .delete('http://localhost:3000/keranjangs/' + item.id)
                    .catch(function (error) {
                        console.log(error);
                    })
                    })

                    this.$router.push({path: "/pesanan-sukses"})
                    this.$toast.success('Sukses dipesan.', {
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
                this.$toast.error('Nama dan Nomor Meja wajib diisi !', {
                            // optional options Object
                            type: 'error',
                            position: 'top-right',
                            duration: 3000,
                            dismissible: true

                        })
            }
            console.log(this.pesan)
        }

    },
    mounted() {
        axios
            .get('http://localhost:3000/keranjangs')
            .then((response) =>
                // handle success
                this.setKeranjang(response.data)
            )
            .catch(function (error) {
                // handle error
                console.log(error);
            })
    },
    computed: {   // computed menjumlahkan
        totalHarga() {
            return this.keranjangs.reduce((items, data) => {
                return items + (data.product.harga * data.jumlah_pemesanan)
            }, 0)
        }
    }
}
</script>

<style>
</style>