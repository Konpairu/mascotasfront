<template>
    <form @submit="onSubmit" class="add-form">
      <div class="form-control">
        <label>Propietario</label>
        <input type="text" v-model="name" name="name" placeholder="Nombre del propietario" />
      </div>
      <div class="form-control">
        <label>Telefono</label>
        <input
          type="text"
          v-model="phone"
          name="phone"
          placeholder="Numero de celular"
        />
      </div>
  
      <input type="submit" value="Guardar Propietario" class="btn btn-block" />
    </form>
  </template>
  
  <script setup>
    import { ref } from 'vue'

    const name  = ref('')   
    const phone = ref('')    

    const emit  = defineEmits(['add-owner'])
        
    function onSubmit(e) {
        e.preventDefault()
        if (!name.value) {
            alert('Sin datos')
            return
        }
        const newOwner = {
            //id: Math.floor(Math.random() * 100000),
            name    : name.value,
            phone   : phone.value,
        }
        emit('add-owner', newOwner)
        name.value    = ''
        phone.value   = ''
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