<script setup>
import dragons from '../assets/js/dragons';
import { ref } from 'vue';

//state
const props = defineProps({
    dragonProps: Object
})


// Denne skal holde det nye navn til formularen
const newName= ref(""); 




// her fortæller jeg hvad denne component emitter
const emit = defineEmits (["nameChange", "DeleteDragon"])

function handleSubmit(){
    emit("nameChange", newName.value, props.dragonProps.id);
}

function handleDelete(id){
    emit('DeleteDragon', props.dragonProps.id)
    
}



</script>

<template>
<article>   

    <svg @click="handleDelete" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="red" d="M7 21q-.825 0-1.412-.587T5 19V6H4V4h5V3h6v1h5v2h-1v13q0 .825-.587 1.413T17 21zM17 6H7v13h10zM9 17h2V8H9zm4 0h2V8h-2zM7 6v13z"/></svg>
   <h3>{{ dragonProps.name  }}</h3>
   <img :src="dragonProps.img_url" alt=""> 
   


   <form @submit.prevent="handleSubmit">
    <label for="betterName">Rename to:</label>
    <input v-model="newName" type="text" placeholder="Better name..." id="betterName" required>
    <input type="submit" value="Update name" />
  </form> 

  
</article>

</template>


<style scoped>
article {
    border: 2px solid red ;
    border-radius: 6px;
    padding: 1rem;
    position: relative;

    svg{
        position: absolute;
        top: 1rem;
        right: 1rem;
        padding: .5rem;
        border-radius: 6px;

    }
    svg :hover{
        background-color: #bbb;
    }

    h3{
        text-align: center;
    }



    img{
        max-width: 100%;
    }

    form{
        display: flex;

    }
    form input:last-of-type {
        background: red;
        padding: 0.5rem 1.5rem;
        border-radius: 6px;
        margin-left: auto;
        border: none;
        color: white;
        font-weight: bold;
        cursor: pointer;

    }
}

</style>