<script setup>
import HeaderBar from '@/Components/HeaderBar.vue';
import {Head} from '@inertiajs/vue3';
</script>

<template>
   <Head title="Landing"/>
   <HeaderBar />
   <div class="w-[1020px] flex flex-col mx-auto items-center py-8 mt-10">
      <img src="https://img.freepik.com/free-photo/welcome-phrase-available-launch-open_53876-124476.jpg" alt="Welcome img" class="w-[600px] object-cover">
      <p class="text-2xl">This is my Midterm Project</p>
   </div>
</template>