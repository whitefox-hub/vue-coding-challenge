
<template>
  <div>
    <input type="text" v-model.trim="texto" placeholder="texto" maxlength="64">

    <br>
    <button type="button" @click="ejecutar()">Ejecutar</button>
    

    <br>
    <h4 v-if="encode.length">Encode Uno: {{encode}}</h4>
    <br>
    <ul>
        <li v-for="value in array_uno">
            {{ value }}
        </li>
    </ul>


    <br>
    <h4 v-if="encode.length"> Encode Uno: {{ array_dos.join("") }}</h4>
    <br>
    <ul>
        <li v-for="value in array_dos">
            {{ value }}
        </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

//--------- props ----------------//
const texto=ref("That's one small step for man, one giant leap for mankind.");
const encode=ref('');
const array_uno = ref([]);

const array_dos = ref([]);


const ejecutar = () => {
    //respuesta 1:
    encode.value = (texto.value.replace(/[^A-Z0-9]/ig, "")).substr(0, 64);
    console.log(encode);

    //respuesta 2:
    array_uno.value= (encode.value).match(/.{1,7}/g);
    console.log('hh',array_uno);

    //respuesta 3:
    var arrayLength = array_uno.value.length;
    for (var i = 0; i <= arrayLength; i++) {
        var mapeo = array_uno.value.map(function (word) {
            return word.substring(i-1, i);
        }).join("");

        if(mapeo.length){
            array_dos.value.push(mapeo);
        }
    }

    console.log(array_dos);
};
</script>
