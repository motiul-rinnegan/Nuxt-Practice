<template>
<h2 class="underline text-center text-sky-400 text-3xl font-bold">Looking for Stylish Wears?</h2>
<div class="p-10 grid grid-cols-1 sm:grid-cols-1 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 gap-5">
    <!--Card 1-->
    <div class="rounded overflow-hidden shadow-lg" v-for="item in fetch">
      <div class="px-6 py-4">

        <img :src="item.image" class="thumb h-48 w-48" alt="product thumb">
        <NuxtLink :to="`/products/${item.id}`"><p class="text-gray-700 text-base">
         <strong>Title</strong> {{item.title}}
        </p></NuxtLink>
         <p class="text-gray-700 text-base">
         <strong>Price</strong> ${{item.price}}
        </p>
        <button type="button" class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Buy Now</button>
        <button type="button" class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Add to Cart</button>
      </div>
      </div>
      </div>
</template>

<script setup lang="ts">
const {data:fetch}=await useFetch(`https://fakestoreapi.com/products?limit=4`);
</script>

<style scoped>

</style>