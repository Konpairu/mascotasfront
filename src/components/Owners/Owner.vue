<template>
    <div :class="['owner']" @click="clickOwner(owner.id)" :style="{border: owner.id == selectedId ? '2px green solid' : ''}">
        <h3>{{ owner.name }}</h3>
        <p>{{ owner.phone }}</p>
    </div>
</template>

<script setup>
    const emit = defineEmits(['selected-owner'])
    defineProps({
        owner: Object,
        selectedId: Number
    })

    function clickOwner(id){
        emit('selected-owner',id)
    }
</script>

<style scoped>
.fas {
  color: red;
}
.owner {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.owner h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>