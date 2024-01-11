<template>
  <menuAdmin />

  <div class="flex justify-between mx-20 mt-5">
    <h1 class="font-bold text-2xl">Propiedades</h1>
    <nuxt-link
      to="/admin/propiedades/create"
      class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
    >
      Crear
    </nuxt-link>
    <hr />
  </div>
  <div class="block w-full overflow-x-auto mx-20 mt-3">
    <table class="items-center bg-transparent w-full border-collapse">
      <thead>
        <tr>
          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Nombre
          </th>
          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Ubicacion
          </th>
          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Habitaciones
          </th>
          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Baños
          </th>
          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          ></th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(categoria, index) in categorias" :key="index">
          <th
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4 text-left text-blueGray-700"
          >
            {{ categoria.name }}
          </th>
          <th
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4 text-left text-blueGray-700"
          >
            {{ categoria.city }}
          </th>
          <th
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4 text-left text-blueGray-700"
          >
            {{ categoria.rooms }}
          </th>
          <th
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4 text-left text-blueGray-700"
          >
            {{ categoria.bathrooms }}
          </th>
          <td
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4"
          >
            <nuxt-link
              :to="'/admin/propiedades/' + categoria.id"
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
            >
              Editar
            </nuxt-link>

            <button
              @click="deleteCate(categoria.id, categoria.name)"
              class="ml-4 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
            >
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import menuAdmin from "@/components/menuAdmin.vue";
import axios from "axios";
import Swal from "sweetalert2";
const categorias = ref([]);
const token = ref(localStorage.getItem("token"));
useHead({
  title: "Categorias",
});

const getCategorias = () => {
  axios.get("https://api-proyectsw.onrender.com/api/properties").then((result) => {
    categorias.value = result.data;
  });
};

getCategorias();

const deleteCate = (id, name) => {
  Swal.fire({
    title: "Error!",
    text: "Desea realmente eliminar: " + name + "?",
    icon: "question",
    showCancelButton: true,
    confirmButtonText: "Eliminar",
    cancelButtonText: "Cancelar",
  }).then((result) => {
    if (result.isConfirmed) {
      ejecutarFuncionConfirmar(id);
    }
  });
};

const ejecutarFuncionConfirmar = (id) => {
  const headers = {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token.value}`,
  };
  axios
    .delete("https://api-proyectsw.onrender.com/api/properties/" + id, { headers })
    .then((result) => {
      getCategorias();
    });
};
</script>