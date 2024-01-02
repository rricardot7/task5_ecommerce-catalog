<template>
    <img class="" :src="image" :alt="title">
</template>

<script>
export default {
    props: {
        image: String,
        title: String
    }
}
</script>