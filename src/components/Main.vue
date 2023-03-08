<script setup>
import { onMounted, ref } from 'vue';
import Header from './Header/Header.vue';
import Pets from './Pets/Pets.vue';
import Owners from './Owners/Owners.vue';
import AddOwner from './Owners/AddOwner.vue';
import AddPet from './Pets/AddPet.vue';

const owners        = ref([])
const pets          = ref([])
const showAddOwner  = ref(false)
const showAddPet    = ref(false)
const selectedOwner    = ref(null)

onMounted(async ()=>{
  await fetchOwners();
  await fetchPets();
})

function fetchPets(){
  if(selectedOwner.value){
    fetch(`api/pets/owner/${selectedOwner.value}`, { method: 'GET' })
          .then(response => response.json())
          .then(data => pets.value = data)
          .catch(error => {
              console.error('Error: Pets Data', error);
              });
  }
}

function fetchOwners(){
   fetch(`api/owners`, { method: 'GET' })
        .then(response => response.json())
        .then(data => owners.value = data)
        .catch(error => {
            console.error('Error: Owners Data', error);
            });
}

function getPets(ownerId){
  selectedOwner.value = ownerId
  fetchPets()
}

function toggleShowingAddOwner(){
  showAddOwner.value = !showAddOwner.value
}
function toggleShowingAddPet(){
  showAddPet.value = !showAddPet.value
}

async function addingOwner(owner){
  await fetch(`api/owners`, {  method: 'POST', 
                                headers:{ 'Content-type': 'application/json'}, 
                                body: JSON.stringify(owner)
                              }
              )
        .then(response => response.json())
        //.then(data => console.log(data))
        .catch(error => {
            console.error('Error: Owners Data', error);
            });
  await fetchOwners()
}

async function addingPet(pet){
  await fetch(`api/pets`, {  method: 'POST', 
                                headers:{ 'Content-type': 'application/json'}, 
                                body: JSON.stringify({...pet, OwnerId:selectedOwner.value})
                              }
              )
        .then(response => response.json())
        //.then(data => console.log(data))
        .catch(error => {
            console.error('Error: Owners Data', error);
            });
  await fetchPets()
}

</script>

<template>
  
    <div class="container">
      
      <Header @click-add="toggleShowingAddOwner()" title="Propietarios" singular="propietario"></Header>
      <div v-show="showAddOwner">
        <AddOwner @add-owner="addingOwner($event)"></AddOwner>
      </div>
      <Owners  @selected-owner="getPets($event)" :owners="owners"></Owners>
      <Header @click-add="toggleShowingAddPet()" title="Mascotas" singular="mascota"></Header>
      <div v-show="showAddPet">
        <AddPet @add-pet="addingPet($event)"></AddPet>
      </div>
      <Pets :pets="pets"></Pets>
    </div>

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
