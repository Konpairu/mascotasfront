<template>
    <h2> Seleccione un propietario </h2>
    <div :key="owner.id" v-for="owner in owners">
        <Owner @selected-owner="ownerClicked($event)" :owner="owner" :selectedId="selectedId"></Owner>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import Owner from '../Owners/Owner.vue';

    const selectedId = ref(null)

    const emit = defineEmits(['selected-owner'])
    defineProps({
        owners: Array
    })

    function ownerClicked(id){
        selectedId.value = id;
        emit('selected-owner',id)
    }
</script>