<template>
    <div class="flex items-center justify-center py-4">
        <button
            class="bg-blue-700 text-black rounded-md cursor-pointer text-xs font-semibold px-3 py-2"
            v-on:click.prevent="addToCart"
        >
            Ajouter au panier
        </button>
    </div>
</template>

<script setup>
import axios from 'axios';

   const productId = defineProps(['productId']);

    const addToCart = async() => {
        await axios.get('/sanctum/csrf-cookie');
        await axios.get('/api/user')
                .then(async(res) => {
                    let response = await axios.post('/api/products', {productId: productId});

                    console.log(res);
                })
                .catch(err => console.log(err.response.data));
    }

</script>