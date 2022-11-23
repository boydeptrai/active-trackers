<template>
  <header class="bg-at-light-green text-white">
    <nav class="container py-5 px-4 flex flex-col items-center gap-4 sm:flex-row" >
        <div class="flex items-center gap-x-4">
          <img src="../assets/images/dumbbell-light.png" class="w-14" alt="">
          <h1 class="text-lg">Active Tracker</h1>
        </div>
        <ul class="flex flex-1 justify-end gap-x-10">
          <router-link class="cursor-pointer " :to="{name: 'Home'}">Home</router-link>
          <router-link v-if="user" class="cursor-pointer " :to="{name: 'Create'}">Create</router-link>
          <router-link v-if="!user" class="cursor-pointer " :to="{name: 'Login'}">Login</router-link>
          <li v-if="user" @click="logout" class="cursor-pointer">Logout</li>
        </ul>
    </nav>
  </header>
</template>

<script>
import {supabase} from '../supabase/init';
import { useRoute } from 'vue-router';
import { computed } from 'vue';
import store from '../store/index'
export default {
  setup() {
    // Get user from store
    const user = computed(() =>store.state.user)
    // Setup ref to router
    const router = useRoute()
    // Logout function
    const logout = async () =>{
     await supabase.auth.signOut();
     router.push({name: "Home"})
    }
    return {logout,user};
  },
};
</script>
