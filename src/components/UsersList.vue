<template>
    <div>
        <div v-for="user in users" :key="user.id">
            <User :user="user"/>
        </div>
    </div>
  
</template>

<script lang="ts">
import User from '@/components/User.vue'
export default {
    props: ['users'],
    components: {
        User
    },
    setup() {

    }
}
</script>

<style>

</style>