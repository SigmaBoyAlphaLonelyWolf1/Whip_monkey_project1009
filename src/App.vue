<template>
  <div class="content">
    <v-card class="mb-3 pa-3" donator-form color="indigo">
      <v-card-item>
        <!-- <label>Troller Name:</label>
        <input placeholder="none" name="Troller_Name" v-model="TrollerName"  /> -->
        <v-text-field label="Troller Name" variant="solo" v-model="TrollerName"></v-text-field>

      </v-card-item>
      <v-card-item>
        <!-- <label>Price:</label>
        <input type="number" name="price" v-model="price" min="1" /> -->
        <v-text-field type="number" min="0.5" label="how much would you donate fatty" variant="solo" v-model="price"></v-text-field>
      </v-card-item>
      <v-card-actions>
        <v-btn variant="outlined" @click="donating" width="100%" >Troll</v-btn>
      </v-card-actions>
    </v-card>
    <div v-if="donatorList.length > 0">
      <h1>total: {{ donatorList.reduce((acc,donator) => acc + donator.price,0) }}</h1>
    </div>
    <v-card class="pa-3" color="deep-purple">
      <v-card-item>
        <v-table class="pa-3 rounded" width="100%">
          <caption>Troller Ranking</caption>
          <thead>
            <tr>
              <th>No.</th>
              <th>TROLLER NAME</th>
              <th>TROLLER PRICE</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="donator in donatorList">
              <td>{{ donator.id }}</td>
              <td>{{ donator.TrollerName }}</td>
              <td>{{ donator.price}}</td>
            </tr>
          </tbody>
        </v-table>

      </v-card-item>
    </v-card>
  </div>
  <v-dialog v-model="dialog.display" max-width="290" persistent>
        <v-btn 
        style="font-size:20px;"
        height="100" @click="dialog.display = false">PLay!</v-btn>
  </v-dialog>
  </template>

<script setup>
import { ref } from 'vue';

const latestDonatorId = ref (0)
const TrollerName = ref('')
const price = ref (1)
const donatorList= ref ([])
const dialog = ref({
  display: true
})

function donating() {

if(TrollerName.value?.length > 0) {
  latestDonatorId.value++
  const donatorDetailTemp = {
    id: latestDonatorId.value,
    TrollerName: TrollerName.value,
    price: price.value
  } 
  donatorList.value.push(donatorDetailTemp)
  donatorList.value.sort((a, b)=> b.id - a.id)
  console.log(donatorList.value)
}else if (TrollerName.value?.length <= 0) {
  alert('Put your name in lil n word')
}

}

</script>

<style>
.content {
  /* display: block; */
  min-width: 800px;
  /* background-color: rgb(168, 133, 35); */
  /* padding: 1rem; */
  /* color: black; */
  /* border-radius: 0.5rem; */
  
}

 body {
   background-image: url(https://preview.redd.it/n3qtt3swuzbb1.jpg?auto=webp&s=604934ad861bc468037e5741c6d32d5093760e4d);
 }
 /* change into this later https://codepen.io/creme/pen/aPJwEz */
</style>

