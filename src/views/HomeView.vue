<template>
  
 
  <div class="home flex items-center bg-slate-50">
    <img alt="Vue logo" class="w-20 h-20 p-4 " src="../assets/logo.png">
    <h1 class="text-3xl font-bold">Hello world</h1>
     
  </div>
  <div class="flex space-x-10">
    <div class="bg-slate-50 w-[18%] my-10 py-4 rounded-xl shadow-md">
      <h3 class="text-md font-bold items-center justify-center text-center py-4">Users</h3>
      <UsersList :users="users" />
      
    </div>
    <UsersTable :users="users" />   
    
  </div>

  <div class="w-1/3 bg-slate-50 items-center justify-center p-10 rounded-xl shadow-lg">
    <form class="space-y-2 flex flex-col" @submit.prevent="addUser">
      <h2>Add / Edit User</h2>
      <label class="text-gray-500 text-sm font-light pr-4 flex-col">Name:</label>
      <input type="text" class="p-2 rounded-md" v-model="newUser.name" required>

      <label class="text-gray-500 text-sm font-light pr-4 flex-col">Email:</label>
      <input type="email" class="p-2 rounded-md" v-model="newUser.email" required>
            

        <label class="text-gray-500 text-sm font-light pr-4">Password:</label>
        <input type="password" class="p-2 rounded-md" v-model="newUser.password" required > 

        <label class="text-gray-500 text-sm font-light pr-4">Verify password:</label>
        <input type="password" class="p-2 rounded-md" v-model="newUser.vPassword" required >
      

      <div class="submit">
          <button type="submit" class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 my-4 rounded">Add new user</button>
      </div>

    </form>

</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import UsersList from '@/components/UsersList.vue'
import UsersTable from '@/components/UsersTable.vue'
import getUsers from '@/composables/getUsers'
import ModalComponent from '@/components/ModalComponent.vue'

interface User {
  id: number,
  name: string,
  email: string,
  password: string,
  vPassword?: string
}

export default defineComponent({
  name: 'home',
  components: {
    UsersList, UsersTable, ModalComponent
  },
  setup() {
    const { users, error, load } = getUsers()
    load()  

    const newUser = ref<User>({
      id:  0,
      name: '',
      email: '',
      password: '',
      vPassword:''
    })

    function addUser() {
      if(newUser.value.password === newUser.value.vPassword) {
        newUser.value.id = users.value.length +  1;
        users.value.push(newUser.value)
        newUser.value = {id:  0, name: '', email: '', password: '',}    
      } else {
        return new Error('Passwords do not match.')
      }
    }

    function removeUser(user: User) {
      users.value = users.value.filter((item) => {
        return user !== item
      })
    }

    return { users, error, newUser, addUser, removeUser }
  }
});
</script>


