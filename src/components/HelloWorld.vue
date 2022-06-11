<template>
  <div class="hello">
    v-model="animalName"
    <input type="text" id="nameInput">
    v-model="imageURL"
    <input type="text" id="imageInput">
    <button @click="postAnimal">POST</button>
    <button @click="getAnimals">GET</button>

    <div>
    v-for="animal in animalArr"
    :key="animal.animalId"
    >
      {{anmial.anmialID}}
      <h1>{{animal.animalName}}</h1>
      <img :src="animal.imageURL">
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data() {
    return {
      animalName: null, 
      imageURL: null,
      animalArr : []
    }
  },
  methods: {
    postAnimal(){
      console.log(this.animalName, this.imageURL)
      axios.request({
        url: "http://127.0.0.1:5000/api/animals",
        method : "POST",
        data : {
          animalName : this.animalName,
          imageURL: this.imageURL
        }
      }).then(()=>{
        this.getAnimals();
      }).catch((error)=>{
        console.log(error);
      })
    },
    getAnimals(){
      console.log("Running GET");
      axios.request({
        url: "http://127.0.0.1:5000/api/animals",
        method: "GET"
    }).then((response)=>{
      console.log(response);
      this.animalArr= response.data
    }).catch((error)=>{
      console.log(error);
    })
  },
  mounted (){
    this.getAnimals();
  },
  }
}
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
