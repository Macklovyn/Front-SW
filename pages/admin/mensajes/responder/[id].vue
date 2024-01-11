<template>
  <div class="bg-white rounded shadow-lg p-4 md:p-8 mb-6 mx-10 mt-5">
    <div class="grid gap-4 gap-y-2 text-sm grid-cols-1 lg:grid-cols-3">
      <div class="text-gray-600">
        <p class="font-medium text-lg">Responder Mensaje</p>
      </div>

      <div class="lg:col-span-2">
        <div class="grid gap-4 gap-y-2 text-sm grid-cols-1 md:grid-cols-5">
          <div class="md:col-span-5">
            <label for="full_name">Respuesta</label>
            <input
              type="text"
              class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
              v-model="response"
            />
          </div>

          <div class="md:col-span-5 text-right">
            <div class="inline-flex items-end">
              <button
                @click="store()"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
              >
                Responder
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
const response = ref("");
const idEdit = ref("");
const router = useRouter();
const route = useRoute();
const token = ref(localStorage.getItem("token"));

const getData = () => {
  axios
    .get("https://api-proyectsw.onrender.com/api/messages/" + route.params.id)
    .then((result) => {
      name.value = result.data.name;
      idEdit.value = result.data.id;
    });
};
const store = () => {
  const playload = {
    name: name.value,
  };

  const headers = {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token.value}`,
  };

  axios
    .put("https://api-proyectsw.onrender.com/api/categories/" + idEdit.value, playload, {
      headers,
    })
    .then((result) => {
      router.push("/admin/categorias");
    });
};

getData();
</script>