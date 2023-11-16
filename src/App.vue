<script>
import axios from 'axios';
import { ref } from 'vue';
import './assets/styles.css';

export default {
  setup() {
    const profile = ref(null);

    const obtenerData = async () => {
      try {
        const response = await axios.get('http://localhost:3000/api/profile');
        profile.value = response.data;
        console.log("Respuesta: ", response);
      } catch (error) {
        console.error('Error al obtener el mensaje:', error);
      }
    };

    obtenerData();

    return {
      profile,
    };
  },
};
</script>

<template>
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Perfil Profesional</title>
    <link rel="stylesheet" href="./assets/styles.css">
  </head>
  <body class="bg-[#872341]">
    <section class="flex-col">
        <h1  class ="text-4xl text-center" v-if="profile">Perfil Profesional: {{ profile.name }} {{ profile.lastname }}</h1>
        <p class="text-2xl italic text-center"> {{ profile.summary }}</p>
        <h2 class="text-2xl text-center">Datos Personales</h2>
        <div class="flex flex-nowrap">
          <p class="flex-1 bg-[#22092C] text-center text-[aliceblue] m-2.5 p-[15px] rounded-lg">Edad: {{profile.age}}</p>
          <p class="flex-1 bg-[#22092C] text-center text-[aliceblue] m-2.5 p-[15px] rounded-lg">Ciudad de origen: {{ profile.city }}</p>
          <p class="flex-1 bg-[#22092C] text-center text-[aliceblue] m-2.5 p-[15px] rounded-lg">Correo: {{ profile.email }}</p>
        </div>
        <div class="text-2xl flex flex-wrap">
          <p class="text-2xl text-center">Red social</p>
          <a href="https://www.instagrm.com/n_kishin/" target="_blank">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Instagram_logo_2022.svg/225px-Instagram_logo_2022.svg.png" alt="" width="30"> 
          </a>
        </div>
    </section>
    <section class="flex w-1/2 p-4">
        <h2  class="text-2xl font-bold mb-4">Intereses</h2>
        <div v-if="profile" class="flex flex-wrap bg-[#872341] p-4 rounded-lg"> 
          <ul>
            <li class="list-inside p-2.5 bg-[#22092C] rounded-lg shadow" v-for="(hobbies, index) in profile.hobbies" :key="index">
              <p class="font-semibold text-[aliceblue]">Nombre: {{ hobbies.name }}</p>
              <p class="text-[aliceblue]">Descripción: {{ hobbies.description }}</p>
            </li>
          </ul>
        </div>
    
    </section>
    <section class="flex p-4 bg-[#22092C]">
        <h2  class="text-2xl font-bold mb-4 text-[aliceblue]">Tabla de herramientas</h2>
        <table class="w-full table-auto">
          <thread class="bg-gray-800 text-white">
            <tr>
              <th class="px-4 py-2">Framework</th>
              <th class="px-4 py-2">Nivel</th>
              <th class="px-4 py-2">Año</th>
            </tr>
          </thread>
          <tbody>
            <tr v-for="(framework, index) in profile.frameworks" :key="index" class="text-center bg-gray-200">
                <td class="border px-4 py-2">{{ framework.name}}</td>
                <td class="borrder px-4 py-2">{{ framework.level }}</td>
                <td>{{ framework.year}}</td>
            </tr>
          </tbody>
        </table>
    </section>
  </body>
  </html>
</template>
