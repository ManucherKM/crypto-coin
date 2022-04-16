<template>
    <div class="card" style="width: 18rem; height: 32vh;">
        <img :src="srcImg" class="card-img-top" :alt="altSrc">
        <div class="card-body">
            <h5 class="card-title text-center">{{ coinName }}</h5>
            <p class="card-text text-center">Цена: {{ coinPrice }} $</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        srcImg: {
            type: String,
            required: true
        },
        altSrc: {
            type: String,
            required: true
        },
        coinName: {
            type: String,
            required: true
        },
        coinPrice: {
            type: String,
            required: true
        },
    }
}
</script>

<style scoped>
.card img {
    width: 50%;
    height: auto;
    margin: 10px auto 10px auto;
}

.card .card-body {
    flex: none;
}

.card {
    justify-content: space-around;
}
</style>