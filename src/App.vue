<template>
  <main>
    <div class="notes">
      <h1>Notes</h1>
      <button class="plusbutton" @click="plusbutton=true">+</button>
    </div>
    <div class="cards-container">
      <div class="card" v-for="note in notes" :style="{backgroundColor :note.backgroundColor}">
        <p class="cardtext">{{ note.text }}</p>
        <p class="date">{{ note.date.toLocaleDateString("en-us") }}</p>
      </div>
    </div>
  <div v-if="plusbutton">
    <div class="overlay">
        <div class="textintake">
          <textarea name="note" id="note" cols="30" rows="10" v-model="newnote">
          </textarea>
          <button class="addtextbutton" @click="addnote">Add Text</button>
          <button class="canceltextbutton" @click="plusbutton=false">Cancel</button>
        </div>
    </div>
  </div>
  </main>
</template>
<script setup>
  import { hasDynamicKeyVBind } from "@vue/compiler-core";
import {ref} from "vue";
  const plusbutton=ref(false);
  const newnote=ref("")
  const notes=ref([])
  function getRandomColor(){
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }
  const addnote = () => {
    notes.value.push({
      id: Math.floor(Math.random() *1000000),
      text:newnote.value,
      date:new Date(),
      backgroundColor: getRandomColor()
    })
    plusbutton.value=false;
    newnote.value="";
  }
</script>