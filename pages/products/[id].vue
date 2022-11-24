<template>
<div class="card">
    <div class="grid grid-cols-2 gap-10">
      <div class="p-7">
        <img :src="`${product.image}`" class="mx-auto my-7 h-60 w-96" />
      </div>
      <div class="p-7">
        <h2 class="text-4xl my-7">{{ product.title }}</h2>
        <p class="text-xl my-7">Price - ${{ product.price }}</p>
        <h3 class="font-bold border-b-2 mb-4 pb-2">Product description:</h3>
        <p class="mb-7">{{ product.description }}</p>
        <button type="button" class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Buy Now</button>
        <button type="button" class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Add to Cart</button>
    </div>
    </div>
  </div>
  <h2 class="text-4xl my-7">More Products</h2>
    <div class="p-10 grid grid-cols-1 sm:grid-cols-1 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 gap-5">
    <!--Card 1-->
    <div class="rounded overflow-hidden shadow-lg" v-for="item in fetch">
      <div class="px-6 py-4">

        <img :src="item.image" class="thumb h-48 w-48" alt="product thumb">
        <p class="text-gray-700 text-base">
         <strong>Title</strong> {{item.title}}
        </p>
         <p class="text-gray-700 text-base">
         <strong>Price</strong> ${{item.price}}
        </p>
        <NuxtLink :to="`/products/${item.id}`"><p class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">See Details</p></NuxtLink>
        <p class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Add to Cart</p>
      </div>
      </div>
      </div>
</template>

<script setup lang="ts">
const {id}=useRoute().params
const uri = 'https://fakestoreapi.com/products/' + id
const {data:product}=await useFetch(uri)
const {data:fetch}=await useFetch(`https://fakestoreapi.com/products`);
</script>

<style scoped>

</style>