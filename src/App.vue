<script setup>
import { ref } from 'vue';

const showContainer=ref(false)
const note=ref('')
const notes=ref([])


// method for collect data 
function randomColor(){
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)"

}
function notesCollector(){
  if (note.value==='' || note.value.lenth>0) { 
    return
  }
  
  notes.value.push({
    id:Math.floor(Math.random()*10),
    text:note.value,
    date:new Date(),
    backgroundColor:randomColor()
  })
  note.value=''
  showContainer.value=false

}
function deleteBtn(index){
  const findElement=notes.value.findIndex((note)=>{
    return note.id===id
  })
  
  return notes.value.splice(findElement,1)
}

</script>
<template>
<section class="overlay" v-show="showContainer">
  <div class="overlay-div">
    <textarea name="note" placeholder="Type here..." v-model="note"></textarea>
    <button class="btn1" @click="notesCollector">Add Note</button>
    <button class="btn2" @click="showContainer=false">Close</button>
  </div>   
</section>
<main>
  <header>
    <h1>Notes</h1>
    <button class="button" @click="showContainer=true">+</button>
  </header>

  <section class="cart-container">
    <div class="cart" v-for="(note,index) in notes" :key="index" :style="{backgroundColor:note.backgroundColor}">
      <button class="delete-btn" @click="deleteBtn(index)">X</button>
      <p class="noteText">{{ note.text }}</p>
      <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
    </div> 
  </section>
</main>
</template>
<style scoped>
main{
  width: 90%;   
  margin: auto;
  padding: 20px;
  text-align: center;
}

header{
  width: 80vw;
  margin: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 5vh;

}

.button{
  background-color: blueviolet;
  width: 3vw;
  height: 3vw;
  border-radius: 100%;
  color: white;
  font-size:2vw;
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

h1{
  font-size: 3vw;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
.cart-container{
  width: 80vw;
  text-align: center;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
}

.cart{
  background-color: yellowgreen;
  height: 230px;
  width: 200px;
  text-align: left;
  display: flex;
  flex-direction: column;
  justify-content:space-between ;
  border-radius: 20px;
  margin-top: 50px;
  padding: 10px;
  margin-right:50px ;
}

.overlay{
  background-color: rgb(33, 26, 26);
  width: 99%;
  height: 98vh;
  position:absolute;
  opacity: 0.9;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.overlay-div{
  width: 35%;
  height: 15vw;
  display: flex;
  flex-direction: column;
  
}
textarea{
  height: 90%;
  border: 2px solid black;
  border-radius:10px;
  padding: 10px;
  font-family: cursive;
  font-size: 1.2vw;
}
.overlay-div>button{
 font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
 letter-spacing: 2px;
 color:white;
 font-size: 15px;
 height: 50px;
 margin-top: 1px;
 border-radius: 10px;
 cursor: pointer;
}
.btn1{
  background-color: blueviolet;
}
.btn2{
  background-color: red;
}
.noteText{
  word-wrap: break-word;
  overflow-wrap: break-word;
  font-family: cursive;
}
.delete-btn{

}
</style>

