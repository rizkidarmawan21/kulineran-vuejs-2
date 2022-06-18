<template>
    <div class="hero">

        <!-- for dekstop -->
        <div class="d-none d-md-block">
            <div class="row mt-3  ">
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicius Food Menu,</strong> <br> In Your Gadged</h2>
                            <p>Let's Choose and Order Your Foods Favorite</p>
                            <button class="btn btn-success">
                                <b-icon-arrow-right /> Order Now
                            </button>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <img src="../../public/assets/images/hero.svg" width="400" alt="" />
                </div>
            </div>
        </div>

        <!-- for mobile -->
        <div class="d-sm-block d-md-none p-3">
            <div class="row mt-3 ">
                <div class="col-md-6">
                    <img src="../../public/assets/images/hero.svg" width="350" alt="" />
                </div>
                <div class="col-md-6 mt-5">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicius Food Menu,</strong> <br> In Your Gadged</h2>
                            <p>Let's Choose and Order Your Foods Favorite</p>
                            <button class="btn btn-success">
                                <b-icon-arrow-right /> Order Now
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HeroComponent',
}
</script>

<style>
</style>