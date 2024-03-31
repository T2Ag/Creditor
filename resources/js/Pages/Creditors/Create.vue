<script setup>
import { useForm } from '@inertiajs/vue3';
import HeaderBar from '@/Components/HeaderBar.vue';
import {Head} from '@inertiajs/vue3';
import { Link } from '@inertiajs/vue3';

const form = useForm({
        last_name: '',
        first_name: '',
        gender: '',
        birth_date: '',
        phone: '',
        address: '',
        credit_limit: '',
   })

const submit = () => {
    form.submit('post', '/creditors')
}

</script>

<template>
   <HeaderBar />
   <Head title="Creditors"/>
      <div class="w-[1020px] mx-auto py-8">
         
         <h2 class="text-4xl text-center">Create Creditor</h2>
         
         <div class="w-[600px] mx-auto">
            <form class="block w-[600px]" @submit.prevent="submit">
               <div class="mb-4">
                  <label for="last_name">Last Name</label>
                  <input type="text" id="last_name" class="block w-full rounded" v-model="form.last_name" required>
               </div>
               <div class="mb-4">
                  <label for="first_name">First Name</label>
                  <input type="text" id="first_name" class="block w-full rounded" v-model="form.first_name" required>
               </div>
               <div class="mb-4">
                  <label for="gender">Gender</label>
                  <select id="gender" class="block w-full rounded" v-model="form.gender" required>
                     <option value="Male">Male</option>
                     <option value="Female">Female</option>
                  </select>
               </div>
               <div class="mb-4">
                  <label for="birth_date">Birth Date</label>
                  <input type="date" id="birth_date" class="block w-full rounded" v-model="form.birth_date" required>
               </div>
               <div class="mb-4">
                  <label for="phone">Phone</label>
                  <input type="text" id="phone" class="block w-full rounded" v-model="form.phone" required>
               </div>
               <div class="mb-4">
                  <label for="address">Address</label>
                  <input type="text" id="address" class="block w-full rounded" v-model="form.address" required>
               </div>
               <div class="mb-4">
                  <label for="credit_limit">Credit Limit</label>
                  <input type="number" id="credit_limit" max="50000" min="5000" class="block w-full rounded" v-model="form.credit_limit" required>
               </div>
               <Link :href="'/creditors'" class="mr-2 p-2 bg-green-800 text-white rounded">Back</Link>
               <button type="submit" class="px-4 py-2 bg-blue-800 text-while hover:bg-blue-600 rounded text-white">Create</button>
               
            </form>
         </div>

      </div>


</template>