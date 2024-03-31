<script setup>

import { Link } from '@inertiajs/vue3';

</script>

<template>
   <div class="bg-gray-900 text-white p-4">
      <div class="w-[1020px] mx-auto flex">
         <h1 class="flex-1 text-xl">Midterm Project</h1>
         <nav class="">

            <Link :href="'/'" class="mx-2 px-4 py-2 hover:bg-gray-700 rounded" :class="{ 'active': $page.url === '/'}">Home</Link>
            <Link :href="'/creditors'" class="mx-2 px-4 py-2 hover:bg-gray-700 rounded" :class="{ 'active': $page.url === '/creditors'}">Creditors</Link>
            <Link :href="'/about'" class="mx-2 px-4 py-2 hover:bg-gray-700 rounded" :class="{ 'active': $page.url === '/about'}">About</Link>

         </nav>
      </div>
   </div>
</template>

<style>  

.active{
   margin: 0, .5rem;
   background-color: rgb(55, 65, 81);
   border-radius: 0.25rem;
}

</style>