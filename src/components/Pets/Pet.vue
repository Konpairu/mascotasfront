<template>
    <div :class="[pet.catdog ? 'catdog':'','pet']">
        <h3>{{ pet.name }}</h3>
        <p>raza: {{ pet.race }}</p>
        <p>familia: {{ pet.family }}</p>
    </div>
</template>

<script setup>
    defineProps({
        pet: Object
    })
</script>

<style scoped>
.fas {
  color: red;
}
.pet {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.pet.catdog {
  border-left: 5px solid green;
}
.pet h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>