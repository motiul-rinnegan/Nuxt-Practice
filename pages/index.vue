<template>
<div class="pb-48 pt-16 bg-teal-500 grid place-items-center h-10">
<div >
    <div class="text-center lg:text-2xl md:text-xl text-lg lg:p-0 p-1 font-black text-gray-700">Search products by their title</div>
<div class="flex flex-col p-2 py-6 m-h-screen">
  <div class="bg-white items-center justify-between w-full flex rounded-full shadow-lg p-2 mb-5 sticky" style="top: 5px">
      <input v-model="search" name="search"  autocomplete="off" @focus="showDiv=true" @input="onClick" class="font-bold uppercase rounded-full w-96 py-4 pl-4 text-gray-700 bg-gray-100 leading-tight focus:outline-none focus:shadow-outline lg:text-sm text-xs" type="text" placeholder="Search"> 
      <div class="bg-gray-600 p-2 hover:bg-blue-400 cursor-pointer mx-2 rounded-full">
              <svg class="w-6 h-6 text-white" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
              </svg>
          </div>
      </div>
      <div v-if="fetchedProducts.length" class="z-40">
        <ul  v-show="showDiv" v-for="filterproduct in fetchedProducts" v-bind:key="filterproduct.title"  @click="setState(filterproduct)" class="font-bold uppercase text-gray-700  w-62 bg-white-800 text-black">
          <li class="border-b cursor-pointer text-gray-700 bg-white">
            {{filterproduct.title}}
          </li>
        </ul>
      </div>
      <div v-else class="z-40">
        <ul class="font-bold uppercase text-gray-700  w-62 bg-white-800 text-black">
          <li class="border-b cursor-pointer text-gray-700 bg-white">
            No Product Found for {{search}}
          </li>
        </ul>
      </div>
  <div class="flex flex-col gap-4 lg:p-4 p-2  rounde-lg m-2">
  </div>
</div>
</div>
</div>
   
<h2 class="underline text-center text-sky-400 text-3xl font-bold">Looking for Stylish Wears?</h2>
<div class="p-10 grid grid-cols-1 sm:grid-cols-1 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 gap-5" @click="showDiv=false">
    <!--Card 1-->
    <div class="rounded overflow-hidden shadow-lg" v-for="item in fetchedProducts" v-bind:key="item.title">
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
      <h2 class="underline text-center text-sky-400 text-3xl font-bold">More Related Products</h2>
<div class="p-10 grid grid-cols-1 sm:grid-cols-1 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 gap-5">
    <!--Card 1-->
    <div class="rounded overflow-hidden shadow-lg" v-for="p in products">
      <div class="px-6 py-4">

        <img :src="p.image" class="thumb h-48 w-48" alt="product thumb">
        <p class="text-gray-700 text-base">
         <strong>Title</strong> {{p.title}}
        </p>
         <p class="text-gray-700 text-base">
         <strong>Price</strong> ${{p.price}}
        </p>
        <NuxtLink :to="`/products/${p.id}`"><p class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">See Details</p></NuxtLink>
        <p class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Add to Cart</p>
      </div>
      </div>
      </div>
</template>

<script setup lang="ts">
const search = ref('');
const {data:fetch}=await useFetch(`https://fakestoreapi.com/products?limit=4`);
const fetchedProducts = computed(() => {
      return fetch.value.filter((item) => {
        return (
          item.title
            .toLowerCase()
            .indexOf(search.value.toLowerCase()) != -1
        );
      });
});
const {data:products}=await useFetch(`https://fakestoreapi.com/products?limit=4`);
const showDiv = ref(false);
const showDiv2 =ref(false);
function setState(filterproduct){
  search.value=filterproduct.title;
  showDiv.value=false;

}
</script>

<style scoped>
 .thumb {
    max-height: 120px;
    max-width: 70%;
    margin: 0 auto;
  }
</style>