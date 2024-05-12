<script setup>
import BaseButton from './base/BaseButton.vue'
import { useCurrentUser, useFirebaseAuth } from 'vuefire'
import { signOut} from '@firebase/auth'

const user = useCurrentUser()
console.log(user)

const auth = useFirebaseAuth()

async function logOut(){
signOut(auth).then(() => {
  // Sign-out successful.
  console.log('User Logged out')
}).catch((error) => {
  // An error happened.
  console.log(error)
});
}
</script>

<template>
  <nav class="pr-4">
    <BaseButton to="/">Home</BaseButton>
    <BaseButton to="/new">New</BaseButton>
    <!-- check if user exists before checking for an email property -->
    <BaseButton @click="logOut" v-if="user?.email">Sign out</BaseButton>
    <BaseButton v-else to="/sign-in">Sign-In</BaseButton>
  </nav>
</template>

<style></style>