<template>
    <div :key="pet.id" v-for="pet in pets">
        <Pet :pet="pet"></Pet>
    </div>
</template>

<script setup>
    import Pet from '../Pets/Pet.vue';

    defineProps({
        pets: Array
    })

</script>