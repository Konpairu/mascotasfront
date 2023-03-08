<template>
    <form @submit="onSubmit" class="add-form">
      <div class="form-control">
        <label>Mascota</label>
        <input type="text" v-model="name" name="name" placeholder="Nombre de la mascota" />
      </div>
      <div class="form-control">
        <label>Raza</label>
        <input
          type="text"
          v-model="race"
          name="race"
          placeholder="Raza de la mascota"
        />
      </div>
      <div class="form-control">
        <label>Familia</label>
        <input
          type="text"
          v-model="family"
          name="family"
          placeholder="Familia de la mascota"
        />
      </div>
  
      <input type="submit" value="Guardar Mascota" class="btn btn-block" />
    </form>
  </template>
  
  <script setup>
    import { ref } from 'vue'

    const name  = ref('')   
    const race = ref('')   
    const family = ref('')    

    const emit  = defineEmits(['add-pet'])
        
    function onSubmit(e) {
        e.preventDefault()
        if (!name.value) {
            alert('Sin datos')
            return
        }
        const newPet = {
            //id: Math.floor(Math.random() * 100000),
            name    : name.value,
            race   : race.value,
            family   : family.value,
        }
        emit('add-pet', newPet)
        name.value    = ''
        race.value   = ''
        family.value   = ''
    }
  </script>
  
  <style scoped>
  .add-form {
    margin-bottom: 40px;
  }
  .form-control {
    margin: 20px 0;
  }
  .form-control label {
    display: block;
  }
  .form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 17px;
  }
  </style>