<template>
  <div>
    <menuAdmin />

    <div class="flex justify-between mx-20 mt-5">
      <h1 class="font-bold text-2xl">Categorias</h1>
      <NuxtLink
        to="/admin/categorias/create"
        class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
      >
        Crear
      </NuxtLink>
      <hr />
    </div>
    <div class="block w-full overflow-x-auto mx-20 mt-3">
      <table class="items-center bg-transparent w-full border-collapse">
        <thead>
          <tr>
            <th
              class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
            >
              Categoria
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
            <td
              class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4"
            >
              <NuxtLink
                :to="'/admin/categorias/' + categoria.id"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
              >
                Editar
              </NuxtLink>

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
  </div>
</template>

<script setup>
import menuAdmin from "@/components/menuAdmin.vue";
import axios from "axios";
import Swal from "sweetalert2";

const categorias = ref([]);
const token = ref(localStorage.getItem("token"));

const getCategorias = () => {
  axios.get("https://api-proyectsw.onrender.com/api/categories")
    .then((result) => {
      categorias.value = result.data;
    })
    .catch((error) => {
      console.error("Error al obtener categorías:", error);
    });
};

const deleteCate = (id, name) => {
  Swal.fire({
    title: "Error!",
    text: "¿Realmente deseas eliminar: " + name + "?",
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

  axios.delete("https://api-proyectsw.onrender.com/api/categories/" + id, { headers })
    .then((result) => {
      getCategorias();
    })
    .catch((error) => {
      console.error("Error al eliminar categoría:", error);
    });
};

onMounted(() => {
  getCategorias();
});

useHead({
  title: "Categorias",
});
</script>
