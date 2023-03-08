<template>
    <header>
        <h1>{{ title }}</h1>
        <Button 
          @click="toggleButton()" 
          :text="closeMode ? 'Close': 'Agregar '+singular " 
          :color="closeMode ? 'red': 'green'" >
        </Button>
        
    </header>
</template>

<script setup>
import { ref } from 'vue';
import Button from './Button.vue'

const emit = defineEmits(['click-add'])
const closeMode = ref(false)

defineProps({
  title: {
    type: String,
    required: true
  },
  singular: {
    type: String,
    required: true
  }
})

function toggleButton(){
  emit('click-add')
  closeMode.value = !closeMode.value
}

</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>