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
    <section class="flex flex-col pt-2 pb-8 mx-auto max-w-7xl">
        <h1  class ="text-4xl text-center font-bold pb-4" v-if="profile">Perfil Profesional: {{ profile.name }} {{ profile.lastname }}</h1>
        <p class="text-2xl italic text-center pb-8"> {{ profile.summary }}</p>
        <h2 class="text-2xl text-center font-semibold">Datos Personales</h2>
        <div class="flex flex-row justify-center items-center">
          <img :src="profile.url_pic" class="w-64 h-64 object-cover rounded-full">
          <div class="pt-8">
            <p class="bg-[#22092C] text-center text-[aliceblue] m-2.5 p-[15px] rounded-lg">Edad: {{profile.age}}</p>
            <p class="bg-[#22092C] text-center text-[aliceblue] m-2.5 p-[15px] rounded-lg">Ciudad de origen: {{ profile.city }}</p>
            <p class="bg-[#22092C] text-center text-[aliceblue] m-2.5 p-[15px] rounded-lg">Correo: {{ profile.email }}</p>
          </div>
          <div class="flex flex-col p-10">
            <p class="text-2xl text-center pr-4 font-semibold">Red social:  </p>
            <a :href="profile.instagram" target="_blank">
              <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Instagram_logo_2022.svg/225px-Instagram_logo_2022.svg.png" alt="" width="30"> 
            </a>
          </div>
        </div>
    </section>
      <section class="flex flex-col p-4 mx-auto max-w-7xl">
          <h2  class="text-2xl font-bold mb-4 text-center">Intereses</h2>
          <div v-if="profile" class="flex flex-wrap bg-[#872341] p-4 rounded-lg justify-center items-center"> 
            <ul>
              <li class="list-inside p-2.5 bg-[#22092C] rounded-lg shadow mb-4" v-for="(hobbies, index) in profile.hobbies" :key="index">
                <p class="font-semibold text-[aliceblue]">Nombre: {{ hobbies.name }}</p>
                <p class="text-[aliceblue]">Descripción: {{ hobbies.description }}</p>
              </li>
            </ul>
          </div>
      
      </section>
      <section class="flex flex-col p-4 bg-[#22092C] items-start pt-8 pb-16">
          <h2  class="text-2xl font-bold mb-4 text-[aliceblue] mx-auto max-w-7xl">Tabla de herramientas</h2>
          <table class="w-1/2 table-fixed mx-auto border-4 border-[#872341]">
            <thead class="bg-[#872341] text-white">
              <tr>
                <th class="text-center">Framework</th>
                <th class="text-center">Nivel</th>
                <th class="text-center">Año</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(framework, index) in profile.frameworks" :key="index" class="text-center bg-white">
                  <td class="border border-[#872341]">{{ framework.name}}</td>
                  <td class="border border-[#872341]">{{ framework.level }}</td>
                  <td class="border border-[#872341]">{{ framework.year}}</td>
              </tr>
            </tbody>
          </table>
      </section>
  </body>
  </html>
</template>
