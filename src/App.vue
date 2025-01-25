    <script setup>
    import { ref } from 'vue';
    const showModel = ref(false);
    const newNotes=ref("");
    const errorMessage=ref("");
    const notes=ref([]);

    function getRandomColor() {
       return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
        
}


    const addNote=()=>{
      if(newNotes.value.length <10){
        return errorMessage.value="Please type 10 characters or More"
      }
      notes.value.push({
        id:Math.random() * 10000,
        text:newNotes.value,
        date:new Date(),
        backgroundColor: getRandomColor(),
        
      });
      showModel.value=false;
      newNotes.value="";
      errorMessage.value=""
    }
    
    </script>


<template>
 <main>

  
  <div v-if="showModel" class="overlay">
    <div class="model">
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <textarea v-model.trim="newNotes" name="note" id="note" cols="30" rows="10"></textarea>
      <button @click="addNote">Add Note</button>
      <button class="close" @click="showModel=false">Close</button>
    </div>
  </div>
  <div class="container">

  
    <header>
      <h1>Notes</h1>
      <button @click="showModel =true">+</button>
    </header>

    <div class="cards-container">
      <div class="card" v-for="note in notes" :key="note.id" :style="{backgroundColor:note.backgroundColor}">
        <p class="main-text">
          {{ note.text }}
        </p>
          <p class="date">
            {{ note.date.toLocaleDateString('en-US') }}
          </p>
        
      </div>
      

    </div>
  </div>
 </main>
</template>


<style  scoped>
main{
  height: 100vh;
  width: 100vw;
  background-color: white;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header{
  display:  flex;
  justify-content: space-between;
  align-items: center;
  color: rgb(21, 20,20);
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
header button{
  width: 50px;
  height: 50px;
  border: none;
  padding: 10px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
}
.cards-container{
  
  display: flex;
  flex-wrap: wrap;
 
  
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;

}
.main-text{
color: black;
text-align: center;
}
.date{
  color: black;
  font-size: 12.5px;
  font-weight: bold;
  text-align: center;

}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgb(0,0,0,0.7);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}
.model{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.model button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.model .close{
  background-color: red;
}
.model p{
  color: red;
}
</style>