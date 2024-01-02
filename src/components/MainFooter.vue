<template>
    <div class="product-footer mt-15">
        <h2 class="font-price" :class="{'primary-blue' : isMenCloth, 'primary-purple' : isWomenCloth}">${{ price }}</h2>
    </div>
</template>

<script>
    export default {
        props: {
            price:Number,
            isMenCloth: {
                type: Boolean,
                required: true
            },
            isWomenCloth: {
                type: Boolean,
                required: true
            }
        }
    }
</script>

<style scoped>
    .font-price {
        font-size: 28px;
        font-style: normal;
        font-weight: 600;
        line-height: normal;
    }

    @media screen and (max-width: 600px) {
        .product-footer{
            display: flex;
            align-items: center;
            justify-content: center;
        }
    }
</style>