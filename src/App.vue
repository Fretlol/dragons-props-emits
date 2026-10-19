<script setup>
import {ref } from "vue";
import dragonData from "./assets/js/dragons"
import Dragon from "./components/Dragon.vue"


// state
const dragons = ref(dragonData)

// function der håndtere event fra dragon
function handleNameChange(newName, id){
  // find den rigtige drage ud fra dens id
  const correctDragon = dragons.value.find(dragon => dragon.id === id);


  // opdater dens navn med newName
  correctDragon.name = newName
}

function handleDeleteDragon(id){
 console.log(id)

 dragons.value = dragons.value.filter(dragon => dragon.id != id)
}




</script>

<template>




  <!-- 16. Ekstra/evt: lav en mulighed for at delete dragerne i DragonComp. Så de sender en anden custom event og App.vue fjerner den relevante drage fra state - hjælp i de kommende trin. Se her: https://youtu.be/uXvypD2gPjw -->

  <!-- 17. Opsæt en deleteknap og opsæt eventlistener på den der kalder en funktion: handleDelete -->

  <!-- 18. handleDelete skal emitte en custom event (deleteDragon) OG sende dragens ID som payload -->

  <!-- 19. I app.vue skal DragonComp nu lytte efter deleteDragon eventet og håndtere dette. Den skal bruge id'et fra den drage der skal slettes og slette den rigtige drage i listen med drager i state i App.vue. Her kan man anvende .filter() metoden -->

  <header>
    <h1>D&D website</h1>
    <h2>
      Your source for DnD dragons. Providing dragon information since 2021.<br />
      Find info about <span>{{ dragons.length }}</span> dragons here.
    </h2>
  </header>
  <main>
  <Dragon @deleteDragon="handleDeleteDragon" @nameChange="handleNameChange"
  :dragonProps= "dragon"
   v-for="dragon in dragons" :key= "dragon.id"  /> 


    
  </main>
</template>

<style scoped>
header {
  text-align: center;
  min-height: 60vh;
  background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.9)),
    url("@/assets/img/bg_dragon.jpg");
  background-size: cover;
  display: grid;
  place-content: center;
  color: white;
}

h1 {
  font-size: 4rem;
}

span {
  color: crimson;
}

main {
  max-width: 1000px;
  margin: 1rem auto;
  padding: 2rem;
  box-shadow: 0 0 3px 1px rgba(0, 0, 0, 0.3);
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  border-radius: 6px;
}

@media screen and (max-width: 1050px) {
  main {
    grid-template-columns: 1fr;
    padding: 5rem;
  }
}
</style>
