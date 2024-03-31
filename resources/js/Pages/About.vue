<script setup>
import HeaderBar from '@/Components/HeaderBar.vue';
import {Head} from '@inertiajs/vue3'
</script>

<template>
   <Head title="About"/>
   <HeaderBar />
      <div class="w-[1020px] mx-auto py-8">
         <h2 class="text-2xl">ABOUT PAGE</h2>
         <div class="flex justify-center">
            <div>
               <div class="font-jomhuria text-[110px] mx-3 bg-gradient-to-r from-purple-900 to-red-500 text-transparent bg-clip-text">
                  <p class="mb-[-6rem] mt-20 ">Hello, I'm </p>
                  <p>Tito Agustin L. Obguia</p>
               </div>
               <div class="w-[560px] mx-5 mt-[-3rem] text-justify text-gray-500">
                  <p>I am a third-year IT student at Mater Dei College, currently residing in the picturesque town of Potohan, Tubigon, Bohol. My passion for technology and programming is what drives me, and I am always eager to explore new aspects of the field.
                     In my free time, I indulge in playing computer games, which not only entertains me but also helps me stay sharp and competitive. I also have a creative side, as I enjoy expressing myself through drawing. Occasionally, I find joy in experimenting with different recipes and cooking up a storm in the kitchen.
                     Programming is more than just a hobby for me; it's a passion. I am constantly seeking to expand my knowledge and skills in this area, driven by a desire to make a positive impact in the world through technology.</p>
               </div>
            </div>
            <div class="ml-20 mt-[11rem]">
               <img src="https://uploads.dailydot.com/2023/11/GigaChad.jpg?q=65&auto=format&w=1600&ar=2:1&fit=crop" alt="Profile Picture" 
               class="rounded-full object-cover " style="width: 270px; height: 270px;">
            </div>
         </div>


      </div>

</template>