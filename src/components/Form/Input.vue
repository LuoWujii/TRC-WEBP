<script setup>
import { ref, computed } from 'vue';
const props = defineProps({
    modelValue: String | Number, 
    type: String | null,
    placeholder: String
})

const emit = defineEmits(['update:modelValue']);

const isShown = ref(false);
const computedInputType = computed(() => {
  return props.type == 'password' ? isShown.value ? 'text' : 'password' : props.type 
});
</script>

<template>
  <div class="relative">
    <input class="bg-inputCol py-5 px-5 text-xs rounded-md w-full"
    :value="modelValue"
    :placeholder="placeholder"
    @input="$emit('update:modelValue', $event.target.value)"
    :type="computedInputType"/>
    <div v-if="type == 'password'">
      <i @click="isShown = !isShown" :class="isShown ? 'fa-eye-slash' : 'fa-eye'" class="fa-regular cursor-pointer absolute top-5 right-6"></i>
    </div>
  </div>
</template>


<style>

</style>