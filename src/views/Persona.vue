<script setup>
import { ref, onMounted } from "vue";
import axios from "axios"

const personas = ref([])
const visible_dialog = ref(false);
const persona = ref({nombres: "", apellidos: "", ci_dni:""})

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

async function funGuardarPersona(){
  
  const {data} = await axios.post('http://127.0.0.1:3000/api/persona', persona.value)
  visible_dialog.value = false;
  persona.value = {}
  listarPersonas();
}

</script>

<template>
  <div class="card">
    
    <h2>Gestión Personas</h2>


    <Button label="Nueva Persona" @click="visible_dialog = true" />

<Dialog v-model:visible="visible_dialog" modal header="Registro de Persona" :style="{ width: '25rem' }">
    <span class="p-text-secondary block mb-5">Ingrese información de Persona.</span>
    <div class="flex align-items-center gap-3 mb-3">
        <label for="nom" class="font-semibold w-6rem">Nombres</label>
        <InputText id="nom" class="flex-auto" autocomplete="off" v-model="persona.nombres" />
    </div>

    <div class="flex align-items-center gap-3 mb-5">
        <label for="ap" class="font-semibold w-6rem">Apellidos</label>
        <InputText id="ap" class="flex-auto" autocomplete="off" v-model="persona.apellidos"/>
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="ci_dni" class="font-semibold w-6rem">CI/DNI</label>
        <InputText id="ci_dni" class="flex-auto" autocomplete="off" v-model="persona.ci_dni" />
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="foto_perfil" class="font-semibold w-6rem">foto_perfil</label>
        <InputText id="foto_perfil" class="flex-auto" autocomplete="off" v-model="persona.foto_perfil" />
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="correo" class="font-semibold w-6rem">correo</label>
        <InputText id="correo" class="flex-auto" autocomplete="off" v-model="persona.correo" />
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="clave" class="font-semibold w-6rem">clave</label>
        <InputText type="password" id="clave" class="flex-auto" autocomplete="off" v-model="persona.clave" />
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="telefono" class="font-semibold w-6rem">telefono</label>
        <InputText id="telefono" class="flex-auto" autocomplete="off" v-model="persona.telefono" />
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="fecha_nacimiento" class="font-semibold w-6rem">fecha_nacimiento</label>
        <InputText type="date" id="fecha_nacimiento" class="flex-auto" autocomplete="off" v-model="persona.fecha_nacimiento" />
    </div>
    <div class="flex align-items-center gap-3 mb-5">
        <label for="genero" class="font-semibold w-6rem">genero</label>
        <InputText id="genero" class="flex-auto" autocomplete="off" v-model="persona.genero" />
    </div>
    <div class="flex justify-content-end gap-2">
        <Button type="button" label="Cancelar" severity="secondary" @click="visible_dialog = false"></Button>
        <Button type="button" label="Guardar" @click="funGuardarPersona()"></Button>
    </div>
</Dialog>

    <DataTable :value="personas" tableStyle="min-width: 50rem">
        <Column field="id" header="ID"></Column>
        <Column field="nombres" header="Nombre Completo"></Column>
        <Column field="ci_dni" header="CI/DNI"></Column>
        <Column field="foto_perfil" header="FOTO PERFIL">
          <template #body="slotProps">
            <Image :src="slotProps.data.foto_perfil" alt="Image" width="50" preview v-if="slotProps.data.foto_perfil" />
            <p v-else>Sin Imagen</p>
          </template>
        </Column>
        <Column field="correo" header="Correo"></Column>

    </DataTable>
<!--
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
    -->
  </div>
</template>

<style scoped>

</style>
