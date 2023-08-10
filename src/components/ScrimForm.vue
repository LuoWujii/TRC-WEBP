<script setup>
import { ref } from 'vue';
import FormGroup from './Form/FormGroup.vue';


const emit = defineEmits(['submit'])
defineProps({
    formType: {
        type: String,
        default: "mpScrim" | "brScrim" | 'scrims'
    }
})

const scrim = ref({
    clanName: '',
    teamName: '',
    teamLeader: '',
    ign: '',
    ign2: '',
    ign3: '',
    ign4: '',
})
const errors = ref({
    clanName: '',
    teamName: '',
    teamLeader: '',
    ign: '',
    ign2: '',
    ign3: '',
    ign4: '',
})
const submitForm = ()=> {
  
    if(scrim.value.clanName == '') {
        errors.value.clanName = 'The clan name is required'
    } else if (scrim.value.teamName == '') {
        errors.value.teamName = 'Team name is required'
    } else if (scrim.value.teamLeader == '') {
        errors.value.teamLeader = 'Team Leader is required'
    } else if (errors.value.ign == '') {
        errors.value.ign = 'IGN is required'
    }
    else if (errors.value.ign2 == '') {
        errors.value.ign2 = 'IGN is required'
    }
    else if (errors.value.ign3 == '') {
        errors.value.ign3 = 'IGN is required'
    }
    else if (errors.value.ign4 == '') {
        errors.value.ign4 = 'IGN is required' || ''
    }


    emit("submit", scrim.value)
    console.log('scrim', scrim.value);
}
</script>

<template>
  <div class=" w-full flex-col flex items-center ">
   <div class="flex  md:p-7  flex-col">
    <h1 class=" hidden md:block text-homeBtn font-Abril text-6xl ">THE RED CONQUEROR</h1>
    <h1 class="my-5 uppercase  text-homeBtn font-Abril text-4xl ">
        {{ formType !== 'brScrim' ? 'multiplayer scrimmage' : 'battle royale scrimmage' }}
    </h1>
   </div>
    <form class=" p-5 max-w-md rounded-2xl bg-black  w-full bg-opacity-[.67] mx-3" @submit.prevent="submitForm">
    
        <FormGroup class="mb-6"
        :error="errors.clanName"
        v-model="scrim.clanName"
        placeholder="Clan Name"
        type="text"/>

        <FormGroup
        :error="errors.teamName"
        v-model="scrim.teamName"
        placeholder="Team Name"
        type="text"/>
        <h1 class="my-5 font-Titillium text-white ">Players</h1>

        <div class="flex justify-center">
            <FormGroup

        v-if="formType == 'mpScrim'"
        :error="errors.teamLeader"
        v-model="scrim.teamLeader"
        placeholder="Team Leader"
        type="text"/>
        </div>
        <div class="flex justify-center gap-6 mt-5 ">
            <FormGroup
            :error="errors.ign"
            v-model="scrim.ign"
            placeholder="IGN"
        type="text"/>
        <FormGroup
        :error="errors.ign2"
        v-model="scrim.ign2"
        placeholder="IGN"
        type="text"/>
    </div>
    <div class="flex justify-center gap-6 mt-5 ">
<FormGroup
:error="errors.ign3"
v-model="scrim.ign3"
placeholder="IGN"
type="text"/>
    <FormGroup
    :error="errors.ign4"
v-model="scrim.ign4"
placeholder="IGN"
type="text"/>
</div>
        <button v-if="formType == 'mpScrim' && 'brScrim'"
    class=" hover:bg-hoverCol duration-300 transition-all p-2 mt-8 bg-buttonColor font-semibold text-white text-sm rounded-md px-16"
     >Submit</button>
     <slot/>
    </form>

  </div>
</template>


<style>

</style>