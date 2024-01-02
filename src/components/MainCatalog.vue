<template>
       <div class="wrapper flex flex-items-center flex-content-center" :class="{'bg-gradient-blue' : isMenCloth, 'bg-gradient-purple' : isWomenCloth, 'bg-gradient-gray': isOtherCategory}">
        <span v-if="isLoading" class="loader"></span>
        <main v-if="!isLoading && data">     
            <div v-if="isMenCloth || isWomenCloth" class="row flex flex-items-center flex-content-center flex-wrap">
                <div class="col-40">
                    <ProductPreview :image="data.image" :title="data.title"/>
                </div>
                <div class="col-60">
                    <MainHeader :title="data.title" :category="data.category" :rating="data.rating" :isMenCloth="isMenCloth" :isWomenCloth="isWomenCloth"/>
                    <hr>
                    <DescriptionProduct :description="data.description"/>
                    <hr>
                    <MainFooter :price="data.price" :isMenCloth="isMenCloth" :isWomenCloth="isWomenCloth"/>    
                    <div class="button-group">
                        <BtnProductCatalog type="primary" class="mr-20" :isMenCloth="isMenCloth" :isWomenCloth="isWomenCloth">Buy Now</BtnProductCatalog>
                        <BtnProductCatalog type="primary-outline" :isMenCloth="isMenCloth" :isWomenCloth="isWomenCloth" v-on:click="nextProduct">Next Product</BtnProductCatalog>
                    </div>
                </div>
            </div>
            <ErrorPage v-else :image="image404" @next-product="nextProduct"/>
        </main>
    </div>
</template>

<script>
import BtnProductCatalog from './BtnProductCatalog.vue';
import ProductPreview from './ProductPreview.vue';
import MainFooter from './MainFooter.vue';
import MainHeader from './MainHeader.vue';
import ErrorPage from './ErrorPage.vue';
import DescriptionProduct from './DescriptionProduct.vue';
import image404 from '../assets/image/404.jpg'

    export default {
        components: {
            BtnProductCatalog,
            ProductPreview,
            MainFooter,
            MainHeader,
            ErrorPage,
            DescriptionProduct
        },
        data() {
            return{
                data: null,
                currentProductID: 1,
                isLoading: false
            }
        },
        methods: {
            async fetchData(currentProductID){
                this.isLoading = true;
                try {
                    const response = await fetch(`https://fakestoreapi.com/products/${currentProductID}`);
                    this.data = await response.json();
                } catch (error) {
                    console.error("Error Fetching Data:", error);
                } finally {
                    this.isLoading = false;
                }
            },
            nextProduct(){
                console.log("v-on:click")
                this.currentProductID++
                if(this.currentProductID > 20){
                    this.currentProductID = 1
                }
                this.fetchData(this.currentProductID);
            }
        },
        mounted(){
            this.fetchData(this.currentProductID);
        },
        computed: {
            isMenCloth(){
                return this.data && this.data.category === `men's clothing`;
            },
            isWomenCloth(){
                return this.data && this.data.category === `women's clothing`;
            },
            isOtherCategory(){
                return this.data && !this.isMenCloth && !this.isWomenCloth;
            }
        },
    }
</script>

<style>
    .wrapper {
        min-height: 100vh;
        padding: 50px;
    }

    main {
        max-width: 1000px;
        border-radius: 10px;
        background: var(--color-white);
        box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    }

    .button-group{
        margin-top: 15px;
        padding: 10px 0px;
        display: flex;
        flex-wrap: nowrap;
    }

    @media screen and (max-width: 600px) {
        .button-group{
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .button-group .mr-20{
            margin-right: 0px;
            margin-bottom: 10px;
        }

    }

    @media only screen and (min-width: 601px) and (max-width: 900px) {
        main{
            min-width: 500px;
        }
        .wrapper{
            flex-wrap: wrap;
        }

        .button-group{
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .button-group .mr-20{
            margin-right: 0px;
            margin-bottom: 10px;
        }
    }
</style>