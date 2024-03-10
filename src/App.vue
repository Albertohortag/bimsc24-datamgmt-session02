<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref } from "vue";



let name = ref("Alberto Horta");
let userInput = ref(""); // Variável para armazenar o texto do input
let contentText = ref([]); // Variável para armazenar o texto que será exibido em content
let sectionName = ref(""); // Para armazenar a seção a ser alterada
let backgroundColor = ref(""); // Para armazenar a cor de fundo selecionada


function increment() { 
  if (userInput.value.trim() !== "") { // Checa se o input não é vazio
  contentText.value.push(userInput.value); // Adiciona o novo texto ao array
  userInput.value = "";
  }
}

function applyBackgroundColor() {
  const section = sectionName.value;
  const color = backgroundColor.value;
  if (section === "navbar" || section === "sidebar" || section === "content") {
    document.getElementById(section).style.backgroundColor = color;
  }
}

</script>


<template>
  
  <!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Albert's Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="navbar">Parametric View - by {{name}} </div>
    <div id="sidebar">
      Menu<br>
      <br>
      <input
      type="text"
      v-model="userInput"
      placeholder="Type something here"
      @keyup.enter="increment"
      ><br>
      <button @click="increment">Submit</button>
      <input
      type="text"
      v-model="sectionName"
      placeholder="navbar, sidebar, content"
      @keyup.enter="applyBackgroundColor"
      ><br>
      <input type="text"
      v-model="backgroundColor"
      placeholder="Type background color"
      @keyup.enter="applyBackgroundColor"
      ><br>
      <button @click="applyBackgroundColor">Change color</button>
    </div>
    <div id="content">
      <div v-for="(text, index) in contentText" :key="index">{{ text }}</div>
    </div>
</body>
</html>
</template>


<style>
body, html {
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

#navbar {
    background-color: #333;
    color: white;
    padding: 20px 0;
    text-align: center;
    height: 20px;
    width: 100%;
}

#sidebar {
    background-color: #ccc;
    padding: 20px;
    position: fixed;
    left: 0;
    text-align: center;
    top: 60px;
    height: calc(100%);
    width: 10%;
    overflow: auto;
}

#content {
    margin-left: 12%;
    padding: 20px;
}

</style>