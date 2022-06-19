<template>
    <div class="pesanan-sukses">
        <!-- <Navbar /> -->
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col text-center">
                    <img src="../../public/assets/images/menunggu.png" width="300" />
                    <h2><strong>Sukses!!</strong></h2>
                    <h4>Pesanan Anda segera diproses <br> Selamat Menunggu</h4>
                    <br>
                    <br>
                    <router-link to="/">
                        <button class="btn btn-success btn-sm">
                            <b>Kembali ke Menu</b>
                        </button>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
// import Navbar from "@/components/NavbarComponent.vue";
export default {
    name: "PesananSuksesView",
    components: {
        // Navbar,
    },
};
</script>

<style>
</style>