<template>
    <div class="wrapper-page-not-found flex flex-content-center flex-items-center">
        <img class="page-404" :src="image" alt="404 Not Found" width="80%">
        <div class="centered flex flex-content-center flex-items-center flex-column">
            <p class="mb-15">This Product is Unavailable to show</p>
            <BtnProductCatalog type="dark-outline" :isButtonProduct="true" @click="nextProduct">Next Product</BtnProductCatalog>
        </div>
    </div>
</template>

<script>
import BtnProductCatalog from './BtnProductCatalog.vue';
    export default {
        components: {
            BtnProductCatalog
        },
        props: {
            image: String       
        },
        methods: {
            nextProduct() {
                this.$emit('next-product');
            }
        }
    }    
</script>

<style>
    .wrapper-page-not-found{
        min-width: 1000px;
        min-height: 400px;
        position: relative;
    }

    .page-404{
        opacity: 0.2;
    }

    .centered {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    @media screen and (max-width: 600px) {
        p{
            text-align: center;
        }
        .wrapper-page-not-found{
            min-width: 100%;
            min-height: 400px;
        }

    }  
</style>
