<script setup>
import NavBar from '@/components/NavBar.vue';
import ScrimForm from '@/components/ScrimForm.vue';
import { ref } from 'vue';

const next = ref(false)

const toggleNext = ()=> {
   next.value = !next.value
   
}



</script>

<template>
  <div class=" w-full h-full">
    <div class="absolute bg-[#4892E9] h-screen w-screen bg-opacity-[0.13] -z-10"></div>
    <div class="page h-screen w-screen bg-cover bg-no-repeat -z-20 absolute bg-center"></div>
    <NavBar>
        <div class=" mr-36 flex justify-end">
            <router-link :to="{name: 'home'}">
         <button class="hidden lg:block bg-homeBtn hover:bg-hoverBtn px-14 text-white rounded-md py-2">
            Home
         </button>
        </router-link>
         <div class="flex justify-center items-center "> 
            <router-link :to="{name: 'home'}">
               <span class="lg:hidden flex h-20 w-20 items-center cursor-pointer">
               <img src="../assets/images/logoL.png" alt="">
            </span>
            </router-link>
         </div>
        </div>
       </NavBar>
         
   <div class="flex">
      <ScrimForm v-if="!next" formType="mpScrim">

            <button  @click="toggleNext"
     class="p-2 px-16 bg-homeBtn hover:bg-hoverBtn transition-all duration-300 rounded-md text-white mt-8 hover:text-hoverCol" >
     Next 
    </button>
         

   </ScrimForm>

    <ScrimForm v-if="next" formType="brScrim" >
      <button 
     class="p-2 px-16 bg-homeBtn hover:bg-hoverBtn transition-all duration-300 rounded-md text-white mt-8 hover:text-hoverCol" >
     Submit 
    </button>
   </ScrimForm>

    
   </div>
  </div>
</template>



<style lang="scss" scoped>
 .page {
    background-image: url('../assets/images/MpScrim.png');
 }
</style>