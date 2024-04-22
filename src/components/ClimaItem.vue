<script setup>
import { defineProps} from "vue";
defineProps({
  text: String,
  icon: {default: null}
})
</script>
<template>
  
<div class="flex items-center gap-2 justify-center">
<component :is="icon"/>
  <span class="text-sm">{{ text }}</span>
  </div>
   
</template>