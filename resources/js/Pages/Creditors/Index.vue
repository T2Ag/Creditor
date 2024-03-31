<script setup>
import { Link, useForm } from '@inertiajs/vue3';
import HeaderBar from '@/Components/HeaderBar.vue';
import { ref } from 'vue';
import {Head} from '@inertiajs/vue3'

const props = defineProps({
    creditor:Array
})

const deleteCreditorId = ref(null);

const setDeleteCreditorId = (id) => {
    deleteCreditorId.value = id;
};

const delCred = () => {
    const delForm = useForm({
        id: deleteCreditorId.value
    });
    delForm.submit('delete', '/creditors/' + deleteCreditorId.value, {
      preserveScroll: true
    });
   
};

const creditors = ref({
      id: '',
      first_name: '',
      last_name: '',
      gender: '',
      birth_date: '',
      phone: '',
      address: '',
      credit_limit: ''
});

const setCreditor = (creditor) => {
   creditors.value = creditor;
};

const editForm = useForm({
      last_name: '',
      first_name: '',
      gender: '',
      birth_date: '',
      phone: '',
      address: '',
      credit_limit: '',
})

const setEditedCreditor = (creditor) => {
      editForm.last_name = creditor.last_name;
      editForm.first_name = creditor.first_name;
      editForm.gender = creditor.gender;
      editForm.birth_date = creditor.birth_date;
      editForm.phone = creditor.phone;
      editForm.address = creditor.address;
      editForm.credit_limit = creditor.credit_limit;
      editForm.id = creditor.id;
   };

const update = () => {
   editForm.submit('put', '/creditors/' + editForm.id, {
      preserveScroll: true
   })
}

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
   <Head title="Creditors"/>
   <HeaderBar />
      <div class="w-[1020px] mx-auto py-8">

         <div class="flex">
            <h2 class="text-4xl flex-1">List of Creditors</h2>
            
            <!-- <Link :href="'/creditors/create'" class="px-4 py-2 bg-blue-800 text-white rounded hover:bg-blue-700">Create Creditor</Link> -->

            <!-- Button Delete Modal -->
            <button type="button" class="btn btn-primary border-0 bg-blue-500 " data-bs-toggle="modal" data-bs-target="#createModal ">
               Create Creditor
            </button>
         </div>
         <div class="grid grid-cols-3">
            <div v-for="creditor in creditor" :key="creditor.id" class="container border border-gray-400 w-[300px] p-4 m-4 rounded flex flex-col">
               <div class="flex-1">
                  <h2 class="text-xl font-bold py-[10px]">{{ creditor.last_name }} {{ creditor.first_name }}</h2>
                  <p class="text-gray-600 h-[70px]">Address: {{ creditor.address }}</p>
                  <p class="text-gray-600 h-[30px] my-2">Credit Limit: {{ creditor.credit_limit }}</p>
               </div>
               <div>

                  <!-- <Link :href="'/creditor/'+ creditor.id" class="flex w-[75px] justify-center items-center py-1 bg-green-800 text-white rounded hover:bg-green-700">
                     
                     <svg class="w-4 h-4 mr-1 text-white fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512">
                        <path d="M288 32c-80.8 0-145.5 36.8-192.6 80.6C48.6 156 17.3 208 2.5 243.7c-3.3 7.9-3.3 16.7 0 24.6C17.3 304 48.6 356 95.4 399.4C142.5 443.2 207.2 480 288 480s145.5-36.8 192.6-80.6c46.8-43.5 78.1-95.4 93-131.1c3.3-7.9 3.3-16.7 0-24.6c-14.9-35.7-46.2-87.7-93-131.1C433.5 68.8 368.8 32 288 32zM144 256a144 144 0 1 1 288 0 144 144 0 1 1 -288 0zm144-64c0 35.3-28.7 64-64 64c-7.1 0-13.9-1.2-20.3-3.3c-5.5-1.8-11.9 1.6-11.7 7.4c.3 6.9 1.3 13.8 3.2 20.7c13.7 51.2 66.4 81.6 117.6 67.9s81.6-66.4 67.9-117.6c-11.1-41.5-47.8-69.4-88.6-71.1c-5.8-.2-9.2 6.1-7.4 11.7c2.1 6.4 3.3 13.2 3.3 20.3z"/>
                     </svg>
                     View
                  </Link> -->

                  <div class="flex">
                     <!-- Button Delete Modal -->
                     <button type="button" class="btn btn-danger border-0 bg-red-500 mr-2" @click="setDeleteCreditorId(creditor.id)" data-bs-toggle="modal" data-bs-target="#deleteModal ">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4">
                           <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                        </svg>
                     </button>

                     <!-- Button View Modal -->
                     <button type="button" @click="setCreditor(creditor)" class="flex items-center border-0 btn btn-success bg-green-500 mr-2" data-bs-toggle="modal" data-bs-target="#viewModal">
                        <svg class="w-4 h-4 text-white fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512">
                           <path d="M288 32c-80.8 0-145.5 36.8-192.6 80.6C48.6 156 17.3 208 2.5 243.7c-3.3 7.9-3.3 16.7 0 24.6C17.3 304 48.6 356 95.4 399.4C142.5 443.2 207.2 480 288 480s145.5-36.8 192.6-80.6c46.8-43.5 78.1-95.4 93-131.1c3.3-7.9 3.3-16.7 0-24.6c-14.9-35.7-46.2-87.7-93-131.1C433.5 68.8 368.8 32 288 32zM144 256a144 144 0 1 1 288 0 144 144 0 1 1 -288 0zm144-64c0 35.3-28.7 64-64 64c-7.1 0-13.9-1.2-20.3-3.3c-5.5-1.8-11.9 1.6-11.7 7.4c.3 6.9 1.3 13.8 3.2 20.7c13.7 51.2 66.4 81.6 117.6 67.9s81.6-66.4 67.9-117.6c-11.1-41.5-47.8-69.4-88.6-71.1c-5.8-.2-9.2 6.1-7.4 11.7c2.1 6.4 3.3 13.2 3.3 20.3z"/>
                        </svg>
                        
                     </button>

                     <!-- Button Edit Modal -->
                     <button type="button" @click="setEditedCreditor(creditor)" class="btn btn-primary border-0 bg-blue-500 "  data-bs-toggle="modal" data-bs-target="#editModal ">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class=" text-white fill-current w-4 h-6">
                           <path d="M410.3 231l11.3-11.3-33.9-33.9-62.1-62.1L291.7 89.8l-11.3 11.3-22.6 22.6L58.6 322.9c-10.4 10.4-18 23.3-22.2 37.4L1 480.7c-2.5 8.4-.2 17.5 6.1 23.7s15.3 8.5 23.7 6.1l120.3-35.4c14.1-4.2 27-11.8 37.4-22.2L387.7 253.7 410.3 231zM160 399.4l-9.1 22.7c-4 3.1-8.5 5.4-13.3 6.9L59.4 452l23-78.1c1.4-4.9 3.8-9.4 6.9-13.3l22.7-9.1v32c0 8.8 7.2 16 16 16h32zM362.7 18.7L348.3 33.2 325.7 55.8 314.3 67.1l33.9 33.9 62.1 62.1 33.9 33.9 11.3-11.3 22.6-22.6 14.5-14.5c25-25 25-65.5 0-90.5L453.3 18.7c-25-25-65.5-25-90.5 0zm-47.4 168l-144 144c-6.2 6.2-16.4 6.2-22.6 0s-6.2-16.4 0-22.6l144-144c6.2-6.2 16.4-6.2 22.6 0s6.2 16.4 0 22.6z"/>
                        </svg>
                     </button>
                  </div>


               </div>
            </div>   
         </div>

      </div>


      <!-- Delete Modal -->
      <div class="modal fade" id="deleteModal" tabindex="-1" aria-labelledby="deleteModalLabel" aria-hidden="true">
         <div class="modal-dialog">
            <div class="modal-content">
               <div class="modal-header">
                  <h1 class="modal-title fs-5" id="deleteModalLabel">Delete Creditor</h1>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
               </div>
               <form id="deleteForm" @submit.prevent="delCred" method="POST">
                  <div class="modal-body">
                     <p>Are you sure you want to delete this creditor?</p>
                  </div>
                  <div class="modal-footer">
                     <button type="button" class="btn btn-secondary text-gray-700" data-bs-dismiss="modal">No</button>
                     <button type="submit" form="deleteForm" class="btn btn-danger text-red-700" data-bs-dismiss="modal">Yes</button>
                  </div>
               </form>
            </div>
         </div>
      </div>

      <!-- View Modal -->
      <div class="modal fade" id="viewModal" tabindex="-1" aria-labelledby="viewModalLabel" aria-hidden="true">
         <div class="modal-dialog modal-lg">
            <div class="modal-content">
               <div class="modal-header" >
                  <h1 class="modal-title fs-5" id="viewModalLabel">Creditor Id#: {{ creditors.id }}</h1>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
               </div>
               <div class="modal-body">
                  <table class="m-5" >
                     <tr><th class=" px-5 py-3 text-start whitespace-nowrap border-r">Name: </th><td class="px-5">{{ creditors.first_name }} {{ creditors.last_name }}</td></tr>
                     <tr><th class=" px-5 py-3 text-start whitespace-nowrap border-r">Gender: </th><td class="px-5">{{ creditors.gender }}</td></tr>
                     <tr><th class=" px-5 py-3 text-start whitespace-nowrap border-r">Birth Date: </th><td class="px-5">{{ creditors.birth_date }}</td></tr>
                     <tr><th class=" px-5 py-3 text-start whitespace-nowrap border-r">Phone: </th><td class="px-5">{{ creditors.phone }}</td></tr>
                     <tr><th class=" px-5 py-3 text-start whitespace-nowrap border-r">Address: </th><td class="px-5">{{ creditors.address }}</td></tr>
                     <tr><th class=" px-5 py-3 text-start whitespace-nowrap border-r">Credit Limit: </th><td class="px-5">{{ creditors.credit_limit }}</td></tr>
                  </table>
               </div>
               <div class="modal-footer">
                  <button type="button" class="btn btn-secondary text-gray-700" data-bs-dismiss="modal">Close</button>
               </div>
            </div>
         </div>
      </div>

      <!-- Create Modal -->
      <div class="modal fade" id="createModal" tabindex="-1" aria-labelledby="createModalLabel" aria-hidden="true">
         <div class="modal-dialog modal-lg">
            <div class="modal-content">
               <div class="modal-header">
                  <h1 class="modal-title fs-5" id="createModalLabel">Modal title</h1>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
               </div>

               <form id="createForm" @submit.prevent="submit" method="POST" class="mx-3 mt-3">

                  <div class="mb-2">
                     <label for="last_name">Last Name</label>
                     <input type="text" id="last_name" class="block w-full rounded" v-model="form.last_name" required>
                  </div>

                  <div class="mb-2">
                     <label for="first_name">First Name</label>
                     <input type="text" id="first_name" class="block w-full rounded" v-model="form.first_name" required>
                  </div>

                  <div class="mb-2">
                     <label for="gender">Gender</label>
                     <select id="gender" class="block w-full rounded" v-model="form.gender" required>
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                     </select>
                  </div>

                  <div class="mb-2">
                     <label for="birth_date">Birth Date</label>
                     <input type="date" id="birth_date" class="block w-full rounded" v-model="form.birth_date" required>
                  </div>

                  <div class="mb-2">
                     <label for="phone">Phone</label>
                     <input type="text" id="phone" class="block w-full rounded" v-model="form.phone" required>
                  </div>
                  <div class="mb-2">
                     <label for="address">Address</label>
                     <input type="text" id="address" class="block w-full rounded" v-model="form.address" required>
                  </div>

                  <div class="mb-2">
                     <label for="credit_limit">Credit Limit</label>
                     <input type="number" id="credit_limit" max="50000" min="5000" class="block w-full rounded" v-model="form.credit_limit" required>
                  </div>

                  <div class="modal-footer">
                     <button type="button" class="btn btn-secondary text-gray-700" data-bs-dismiss="modal">Cancel</button>
                     <button type="submit" form="createForm" class="btn btn-danger text-red-700" data-bs-dismiss="modal">Create</button>
                  </div>
               </form>
            </div>
         </div>
      </div>

      <!-- Edit Modal -->
      <div class="modal fade" id="editModal" tabindex="-1" aria-labelledby="editModalLabel" aria-hidden="true">
         <div class="modal-dialog modal-lg">
            <div class="modal-content">
               <div class="modal-header">
                  <h1 class="modal-title fs-5" id="editModalLabel">Modal title</h1>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
               </div>

               <form id="editForm" @submit.prevent="update" method="POST" class="mx-3 mt-3">

                  <div class="mb-2">
                     <label for="last_name">Last Name</label>
                     <input type="text" id="last_name" class="block w-full rounded" v-model="editForm.last_name" required>
                  </div>

                  <div class="mb-2">
                     <label for="first_name">First Name</label>
                     <input type="text" id="first_name" class="block w-full rounded" v-model="editForm.first_name" required>
                  </div>

                  <div class="mb-2">
                     <label for="gender">Gender</label>
                     <select id="gender" class="block w-full rounded" v-model="editForm.gender" required>
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                     </select>
                  </div>

                  <div class="mb-2">
                     <label for="birth_date">Birth Date</label>
                     <input type="date" id="birth_date" class="block w-full rounded" v-model="editForm.birth_date" required>
                  </div>

                  <div class="mb-2">
                     <label for="phone">Phone</label>
                     <input type="text" id="phone" class="block w-full rounded" v-model="editForm.phone" required>
                  </div>
                  <div class="mb-2">
                     <label for="address">Address</label>
                     <input type="text" id="address" class="block w-full rounded" v-model="editForm.address" required>
                  </div>

                  <div class="mb-2">
                     <label for="credit_limit">Credit Limit</label>
                     <input type="number" id="credit_limit" max="50000" min="5000" class="block w-full rounded" v-model="editForm.credit_limit" required>
                  </div>

                  <div class="modal-footer">
                     <button type="button" class="btn btn-secondary text-gray-700" data-bs-dismiss="modal">Cancel</button>
                     <button type="submit" form="editForm" class="btn btn-success text-green-700" data-bs-dismiss="modal">Save</button>
                  </div>
               </form>
            </div>
         </div>
      </div>
</template>