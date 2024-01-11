<template>
  <div class="bg-white rounded shadow-lg p-4 md:p-8 mb-6 mx-10 mt-5">
    <div class="grid gap-4 gap-y-2 text-sm grid-cols-1 lg:grid-cols-3">
      <div class="text-gray-600">
        <p class="font-medium text-lg">Crear Propiedad</p>
      </div>

      <div class="lg:col-span-2">
        <div class="grid gap-4 gap-y-2 text-sm grid-cols-1 md:grid-cols-5">
          <div class="md:col-span-5">
            <label for="full_name">Categoria</label>
            <select
              v-model="property.categoryId"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              id=""
            >
              <option value="">SELECCIONE</option>
              <option
                v-for="(categoria, index) in categorias"
                :key="index"
                :value="categoria.id"
              >
                {{ categoria.name }}
              </option>
            </select>
          </div>

          <div class="md:col-span-5">
            <label for="full_name">Nombre</label>
            <input
              type="text"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              v-model="property.name"
            />
          </div>

          <div class="md:col-span-5">
            <label for="full_name">Ciudad</label>
            <input
              type="text"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              v-model="property.city"
            />
          </div>

          <div class="md:col-span-5">
            <label for="full_name">Habitaciones</label>
            <input
              type="text"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              v-model="property.rooms"
            />
          </div>

          <div class="md:col-span-5">
            <label for="full_name">Baños</label>
            <input
              type="text"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              v-model="property.bathrooms"
            />
          </div>

          <div class="md:col-span-5">
            <label for="full_name">Imagen</label>
            <input
              type="text"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              v-model="property.image"
            />
          </div>

          <div class="md:col-span-5 text-right">
            <div class="inline-flex items-end">
              <button
                @click="store()"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
              >
                Crear
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
const property = ref({
  categoryId: "",
  name: "",
  name: "",
  city: "",
  rooms: "",
  bathrooms: "",
  image: "",
});
const router = useRouter();
const token = ref(localStorage.getItem("token"));
const store = () => {
  const headers = {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token.value}`,
  };

  axios
    .post("https://api-proyectsw.onrender.com/api/properties", property.value, { headers })
    .then((result) => {
      router.push("/admin/propiedades");
    });
};

const categorias = ref([]);
const getCategorias = () => {
  axios.get("https://api-proyectsw.onrender.com/api/categories").then((result) => {
    categorias.value = result.data;
  });
};
getCategorias();
</script>