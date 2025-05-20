<script setup>
import { ref, onMounted } from "vue";

const personas = ref([])

onMounted(() => {
  listarPersonas()
})

function listarPersonas(){
  fetch('http://127.0.0.1:3000/api/persona')
      .then(response => response.json())
      .then(json => {
        personas.value = json;
      })
}

</script>

<template>
  <div class="card">
    
    <h2>Gestión Personas</h2>

    <DataTable :value="personas" tableStyle="min-width: 50rem">
        <Column field="id" header="ID"></Column>
        <Column field="nombres" header="Nombre Completo"></Column>
        <Column field="ci_dni" header="CI/DNI"></Column>
        <Column field="foto_perfil" header="FOTO PERFIL"></Column>
        <Column field="correo" header="Correo"></Column>

    </DataTable>

    <table border="1">
      <thead>
        <tr>
          <th>ID</th>
          <th>NOMBRE COMPLETO</th>
          <th>CI/DNI</th>
          <th>FOTO PERFIL</th>
          <th>CORREO</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="per in personas">
          <td>{{ per.id }}</td>
          <td>{{ per.nombres }} {{ per.apellidos }}</td>
          <td>{{ per.ci_dni }}</td>
          <td>
            <img :src="per.foto_perfil" alt="" width="80px">
          </td>
          <td>{{ per.correo }}</td>
          <td>
            <button>editar</button>
            <button>eliminar</button>
          </td>
        </tr>
      </tbody>

    </table>
  </div>
</template>

<style scoped>

</style>
