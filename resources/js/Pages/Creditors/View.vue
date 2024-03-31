<script setup>

import HeaderBar from '@/Components/HeaderBar.vue';
import { useForm } from '@inertiajs/vue3';
import { Link } from '@inertiajs/vue3';
import {Head} from '@inertiajs/vue3'
import { ref } from 'vue';

   const props = defineProps({
      creditor: Object
   })

   const showEdit = ref(false)

   const form = useForm({
        last_name: props.creditor.last_name,
        first_name: props.creditor.first_name,
        gender: props.creditor.gender,
        birth_date: props.creditor.birth_date,
        phone: props.creditor.phone,
        address: props.creditor.address,
        credit_limit: props.creditor.credit_limit,
   })

   const submit = () => {
    
    form.submit('put','/creditors/' + props.creditor.id, {
        onSuccess: () => {
            showEdit.value = false;
        }
    })
    }

    const delForm = useForm({
        id: props.creditor.id
    })

    const delCred = () => {
        const del = confirm("Are you sure you want to delete this Creditor?")
        if(del)
            delForm.submit('delete', '/creditors/' + props.creditor.id)
    }

</script>

<template>
   <Head title="Creditors"/>
   <HeaderBar />
    <div class="p-8 mx-auto max-w-xl">
        
        <h1 class="text-4xl mb-10">Property Details</h1>
        <div class="border border-green-400 rounded shadow">
            <table class="m-5"  v-if="!showEdit">
                <tr><th class=" px-5 py-5 text-start whitespace-nowrap border-r">Name: </th><td class="px-5">{{ creditor.first_name }} {{ creditor.last_name }}</td></tr>
                <tr><th class=" px-5 py-5 text-start whitespace-nowrap border-r">Gender: </th><td class="px-5">{{ creditor.gender }}</td></tr>
                <tr><th class=" px-5 py-5 text-start whitespace-nowrap border-r">Birth Date: </th><td class="px-5">{{ creditor.birth_date }}</td></tr>
                <tr><th class=" px-5 py-5 text-start whitespace-nowrap border-r">Phone: </th><td class="px-5">{{ creditor.phone }}</td></tr>
                <tr><th class=" px-5 py-5 text-start whitespace-nowrap border-r">Address: </th><td class="px-5">{{ creditor.address }}</td></tr>
                <tr><th class=" px-5 py-5 text-start whitespace-nowrap border-r">Credit Limit: </th><td class="px-5">{{ creditor.credit_limit }}</td></tr>
            </table>

            <div class="m-5" v-if="showEdit">
                <form @submit.prevent="submit">
                    <div class="mb-3">
                        <label for="last_name">Last Name</label>
                        <input type="text" id="last_name" class="w-full" v-model="form.last_name">
                    </div>
                    <div class="mb-3">
                        <label for="first_name">First Name</label>
                        <input type="text" id="first_name" class="w-full" v-model="form.first_name">
                    </div>
                    <div class="mb-3">
                        <label for="gender">Gender</label>
                        <select id="gender" class="w-full" v-model="form.gender">
                            <option value="Male">Male</option>
                            <option value="Female">Female</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label for="birth_date">Birth Date</label>
                        <input type="date" id="birth_date" class="w-full" v-model="form.birth_date">
                    </div>
                    <div class="mb-3">
                        <label for="phone">Phone Number</label>
                        <input type="text" id="phone" class="w-full" v-model="form.phone">
                    </div>
                    <div class="mb-3">
                        <label for="address">Address</label>
                        <input type="text" id="address" class="w-full" v-model="form.address">
                    </div>
                    <div class="mb-3">
                        <label for="credit_limit">Credit Limit</label>
                        <input type="number" id="credit_limit" class="w-full" v-model="form.credit_limit">
                    </div>
                    
                    <button type="submit" class="bg-blue-600 text-white py-2 px-4 rounded" >Save Changes</button>
                    
                </form>
                </div>

               <Link :href="'/creditors'" class="m-5 p-2 bg-green-800 text-white rounded">Back</Link>

               <button class="my-5 px-4 py-2 bg-blue-200 rounded " 
                  @click="showEdit = !showEdit"> {{ showEdit ? 'Cancel' : 'Edit'}}
               </button>

               <button class="px-4 py-2 bg-red-600 rounded m-5 text-white" @click="delCred"> Delete </button>
        </div>
    </div>
</template>