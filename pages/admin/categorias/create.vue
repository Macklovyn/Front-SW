<template>
  <div class="bg-white rounded shadow-lg p-6 md:p-10 mb-6 mx-10 mt-5">
    <div class="grid gap-6 text-sm grid-cols-1 lg:grid-cols-3">
      <div class="text-gray-600">
        <p class="font-medium text-lg">Crear Categoría</p>
      </div>

      <div class="lg:col-span-2">
        <div class="grid gap-6 grid-cols-1 md:grid-cols-2">
          <div>
            <label for="category_name" class="block text-sm font-medium text-gray-600">Nombre de la Categoría</label>
            <input
              id="category_name"
              type="text"
              v-model="name"
              class="mt-1 p-3 w-full border border-gray-300 rounded-md focus:ring-blue-500 focus:border-blue-500"
            />
          </div>

          <div class="flex items-center justify-end">
            <button
              @click="store"
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg"
            >
              Crear
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
import { useRouter } from "vue-router";

const name = ref("");
const router = useRouter();
const token = ref(localStorage.getItem("token") || "");

const store = () => {
  if (!name.value.trim()) {
    console.error("El nombre de la categoría no puede estar vacío");
    return;
  }

  const payload = {
    name: name.value,
  };

  const headers = {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token.value}`,
  };

  axios
    .post("https://api-proyectsw.onrender.com/api/categories", payload, { headers })
    .then(() => {
      router.push("/admin/categorias");
    })
    .catch((error) => {
      console.error("Error al crear la categoría:", error);
      // Puedes manejar el error de otra manera, por ejemplo, mostrando un mensaje al usuario.
    });
};
</script>
