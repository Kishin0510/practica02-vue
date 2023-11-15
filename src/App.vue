<script>
import axios from 'axios';


export default {
  data() {
    return {
      profile: null,
    };
  },
  mounted() {
    this.obtenerData();
  },
  methods: {
    async obtenerData() {
      try {
        const response = await axios.get('http://localhost:3000/api/profile');
        this.profile = response.data;
        console.log("Respuesta: ", response);
      } catch (error) {
        console.error('Error al obtener el mensaje:', error);
      }
    },
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
  <body>
    <head>
      <h1 v-if="profile">Perfil Profesional: {{ profile.name }} {{ profile.lastname }}</h1>
      <p>Estudiante de Ingeniería en Computación e Informática en la Universidad Católica del Norte</p>
    </head>
    <section>
        <h2>Datos Personales</h2>
        <div class="flex flex-wrap">
          <p class="flex-1 bg-[#bf4a4a] text-center text-[aliceblue] m-2.5 p-[15px]">Edad: 25 años</p>
          <p class="flex-1 bg-[#bf4a4a] text-center text-[aliceblue] m-2.5 p-[15px]">Ciudad de origen: Antofagasta</p>
          <p class="flex-1 bg-[#bf4a4a] text-center text-[aliceblue] m-2.5 p-[15px]">correo: nicolas.tapia02@alumnos.ucn.cl</p>
        </div>
        <p>Red social:</p>
        <a href="https://www.instagram.com/n_kishin/" target="_blank">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Instagram_logo_2022.svg/225px-Instagram_logo_2022.svg.png" alt="" width="30"> 
        </a>
    </section>
    <section>
        <h2>Intereses</h2>
        <div class="flex flex-wrap"> 
            <ol>
                <li class="list-inside p-2.5">Mi pareja</li>
                <li class="list-inside p-2.5">Videojuegos</li>
                <li class="list-inside p-2.5">Programar</li>
                <li class="list-inside p-2.5">Dibujar</li>
            
            </ol>
        </div>
    
    </section>
    <section>
        <h2>Tabla de herramientas</h2>
        <table>
            <tr>
                <th>Herramienta</th>
                <th>Lenguaje</th>
                <th>Conocimiento</th>
            </tr>
            <tr>
                <td>Visual Studio Code</td>
                <td>JS,Py,Java, C++,HTML,CSS</td>
                <td>Avanzado</td>
            </tr>
            <tr>
                <td>PyCharm</td>
                <td>JS,HTML,CSS</td>
                <td>Medio</td>
            </tr>
            <tr>
                <td>Eclipse</td>
                <td>Java</td>
                <td>Bajo</td>
            </tr>
        </table>
    </section>
  </body>
  </html>
</template>
