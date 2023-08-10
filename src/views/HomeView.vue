<script setup>
import {computed, ref} from 'vue'
import BigText from '@/components/BigText.vue';
import NavBar from '@/components/NavBar.vue';
import RegisterForm from '@/components/RegisterForm.vue';
import Modal from '@/components/Modal.vue';


const open = ref(false)
const icon = ref(false)
const logIn = ()=> {
  passwordError.value = password.length > 7 ? '' : 'Password must be at least 8 Characters';
}
const toggleIcon = ()=> {
  icon.value = !icon.value
}
const username = ref('')
const password = ref('')
const passwordError = ref('')
const visibility = ref('password')
const showPass = () => {
   visibility.value = visibility.value === 'password' ? 'text' : 'password';

   toggleIcon()
}
const toggleMenu = () => {
    open.value = !open.value
}
const openModal = ref(false)

const toggleModal = () => {
  openModal.value = !openModal.value
}

defineProps({
  openModal: {
    type: Boolean,
    default: false,
  }
})


</script>

<template>
  
  <div class="h-full w-full ">

    <Modal  v-if="openModal" @close-modal="toggleModal" v-bind="openModal" />
    <div class="page h-screen w-screen bg-no-repeat bg-cover -z-20 absolute bg-center"></div>
    <div class="absolute bg-[#4892E9] h-screen w-screen bg-opacity-[0.13] -z-10"></div>
    
   <NavBar @toggle-menu="toggleMenu">
    
 <div >
  <ul class="lg:flex lg:items-center lg:px-0 px-10 lg:pb-0 pb-10   
              lg:static absolute lg:w-auto w-full left-0 mr-52
                bg-black lg:bg-opacity-0 bg-opacity-[.67] z-10
                
                 transition-all  ease-in duration-700" :class="[open ? 'top-20' : 'top-[-50%]' ]">

                <li class=" mx-5  my-10 lg:my-0">
                    <button class="text-white px-7 py-3 font-semibold bg-buttonColor rounded-xl 
                    hover:bg-hoverCol duration-500" href="#"
                    @click="toggleModal">Scrimmage</button>
                </li>
                <li class="mx-5  my-10 lg:my-0">
                    <button class="text-white py-3 px-9 font-semibold bg-buttonColor rounded-xl
                    hover:bg-hoverCol duration-500" href="#">AboutUs</button>
                </li>
                
      </ul>
 </div>
 
   </NavBar>
   <div class="flex justify-center">

     <BigText />
     <RegisterForm formType="login" />
     
    
     
   </div>
  </div>
</template>

<style scoped>
.page {
   background-image: url('../assets/images/mainPage.png');

   /* background-image: url('../assets/images/bgGif.gif'); */
}
[ripple] .ripple--container .ripple--body {
  opacity: 0.5 !important;
  background-color: rgba(0, 0, 0, 0.1) !important;
  -webkit-animation: rippler 1000ms;
          animation: rippler 1000ms;
}
</style>