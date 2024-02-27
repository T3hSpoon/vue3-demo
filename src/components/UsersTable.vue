<template>
    <div class="py-10 space-y-4">

        <nav>
            <router-link to="/">Home</router-link> >
            <router-link to="/users">Users</router-link>    
      </nav> 

        <button class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded" @click="toggleModal">Add User</button>
        <div class="bg-slate-50 space-y-4 rounded-xl shadow-md p-10">

            <table class="min-w-[600px] w-full divide-y divide-gray-400 shadow-sm border-gray-400 border text-sm">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-gray-400">
                    <tr v-for="user in users" :key="user.id" >
                        <td>{{ user.name }}</td>
                        <td>{{ user.email }}</td>
                        <td><button class="text-xs text-blue-700" @click="removeUser"> Delete user</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
  
</template>

<script>
import User from '@/components/User.vue'
import getUsers from '@/composables/getUsers'

export default {
    props: ['users'],
    data() {
        return {
            showModal: false,
            toggleModal: false,
           
        }
    },
    components: {
        User
    },
    methods: {
        toggleModal() {
            this.showModal = !this.showModal
        },
        
    }

}
</script>

<style>

</style>