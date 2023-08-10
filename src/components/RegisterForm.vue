<script setup>
import { reactive, ref } from 'vue';
import { defineAsyncComponent } from 'vue';
import LinkImage from '../components/LinkImage.vue';
 const FormGroup = defineAsyncComponent(()=> 
 import('./Form/FormGroup.vue'))

 const props = defineProps({
  formType: {
    type: String,
    default: 'signup' || 'submit' || 'login'
  },
  
 })

 

 const emit = defineEmits(['submit'])

 

 const user = ref ({
    firstName: '',
    lastName: '',
    ign: '',
    email: '',
    password: '',
    confirmPassword: ''
 })
 const errors = ref ({
    firstName: '',
    lastName: '',
    ign: '',
    email: '',
    password: '',
    confirmPassword: ''
 })

 
 
 const submitForm = ()=> {

 if(user.value.firstName == '') {
  errors.value.firstName = 'The First Name is required'
}
else if ( user.value.lastName == '') {
  errors.value.lastName = 'The Last Name is required '
} 
else if ( user.value.ign == '') {
  errors.value.ign = 'IGN is required'
} 
else if ( user.value.email == '') {
  errors.value.email = 'Email is required'
} 
// else if (!/^[^@]+@\w+(\.\w+)+\w$/.test(user.value.email)) {
//         errors.value.email = 'Invalid email';
// } 
else if (user.value.password == '') {
  errors.value.password = 'Password is required'
} 
else if ( user.value.password.length < 8) {
  errors.value.password = 'Password must be at least 8 Characters '
} 
else if (user.value.confirmPassword !== user.value.password ) {
  errors.value.confirmPassword = 'The password must be the same'
}




    emit("submit", user.value)
    console.log('user', user.value);
 }
 
</script>


<template>
  <div class="w-full flex justify-center">
    <form class=" p-5 max-w-md rounded-2xl mt-8 md:mt-28 bg-black  w-full bg-opacity-[.67] mx-3" @submit.prevent="submitForm">

<div class="flex justify-center gap-2">

  <div v-if="formType == 'login'" class="flex justify-center">
    <span class="flex justify-center m-auto">
      <img class="h-36 w-36" src="../assets/images/logoL.png" alt="">
    </span>
  </div>
    <FormGroup class="w-full"
    v-if="formType == 'signup'"
    v-model="user.firstName" 
    :error="errors.firstName"
    placeholder="First name" 
    type="text" />

    <FormGroup 
    class="w-full"
    v-if="formType == 'signup'"
    v-model="user.lastName" 
    :error="errors.lastName"
    placeholder="Last name" 
    type="text" />
</div>
<FormGroup  
v-if="formType == 'signup'"
class="mt-7"
v-model="user.ign" 
:error="errors.ign"
placeholder="IGN" 
type="text" />

<FormGroup  class="my-7"
v-model="user.email" 
:error="errors.email"
placeholder="Email" 
type="email" />

<FormGroup 

v-model="user.password" 
:error="errors.password"
placeholder="Password" 
type="password" />

<FormGroup 
v-if="formType == 'signup'"
class="my-7"
v-model="user.confirmPassword" 
:error="errors.confirmPassword"
placeholder="Confirm Password" 
type="password" />


<div class="mx-8 mt-8">
    <button v-if="formType !== 'login'"
    class=" p-2 bg-buttonColor font-semibold text-white text-sm rounded-md px-16"
     >{{ formType == 'signup' ? "Sign Up" : "Submit" }}</button>
</div>
<div class="mx-8 mt-8">
    <button @click="submitForm" v-if="formType == 'login'"
    class=" p-2 bg-homeBtn font-semibold text-white text-sm rounded-md px-16"
     >{{ formType == 'login' ? "Log In" : "Submit" }}</button>
</div>
<p  v-if="formType == 'login'" class="my-5 cursor-pointer text-white decoration-solid decoration-white underline ">Forgot Password?</p>

<div v-if="formType == 'login'" class=" border-t border-inputCol">

  <router-link :to="{name: 'register'}">
    <button v-if="formType == 'login'"
    class=" p-2 mt-8 bg-buttonColor font-semibold text-white text-sm rounded-md px-16"
     >{{ formType == 'login' ? "Sign Up" : "Submit" }}</button>
  </router-link>

     <p class="text-white m-1 mt-2-" >or</p>

  <LinkImage />
   
</div>
</form>
  </div>
</template>



<style>

</style>