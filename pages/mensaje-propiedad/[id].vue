<template>
  <div class="min-h-screen p-6 bg-gray-100 flex items-center justify-center">
    <div class="container max-w-screen-lg mx-auto">
      <div>
        <h2 class="font-semibold text-xl text-gray-600 mb-4">
          Contacto a {{ itemData.name }}
        </h2>
        <p class="text-gray-500 mb-6">
          Envíanos tu mensaje y lo responderemos lo antes posible.
        </p>

        <div class="bg-white rounded shadow-lg p-4 px-6 md:p-8 mb-6">
          <div class="grid gap-4 gap-y-2 text-sm grid-cols-1 lg:grid-cols-2">
            <div class="text-gray-600">
              <p class="font-medium text-lg">Mensaje</p>
            </div>

            <div class="lg:col-span-1">
              <label for="title" class="block text-sm font-medium text-gray-700">
                Título
              </label>
              <input
                type="text"
                id="title"
                v-model="title"
                class="mt-1 p-2 border border-black rounded-md w-full focus:outline-none focus:border-blue-500"
              />
            </div>

            <div class="lg:col-span-2">
              <label for="content" class="block text-sm font-medium text-gray-700">
                Mensaje
              </label>
              <textarea
                id="content"
                rows="5"
                v-model="content"
                class="mt-1 p-2 border border-black rounded-md w-full focus:outline-none focus:border-blue-500"
              ></textarea>
            </div>

            <div class="lg:col-span-2 text-right">
              <button
                @click="mensaje"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-full focus:outline-none"
              >
                Enviar
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

const title = ref("");
const content = ref("");
const token = ref(localStorage.getItem("token"));

const router = useRouter();
if (!localStorage.getItem("sesion")) {
  router.push("/auth/login");
  console.log("no tiene sesión");
}
const route = useRoute();

const itemData = await $fetch(
  `https://api-proyectsw.onrender.com/api/properties/${route.params.id}`
);

console.log(itemData);
useHead({
  title: `Mensaje a propiedad: ${itemData.name}`,
});

const mensaje = async () => {
  const playload = {
    content: content.value,
    title: title.value,
    propertyId: itemData.id,
  };
  const headers = {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token.value}`,
  };
  axios
    .post("https://api-proyectsw.onrender.com/api/messages", playload, { headers })
    .then((result) => {
      if (result.data.status == 200) {
        router.push("/admin/");
      }
    });
};
</script>

<style scoped>
/* Estilos específicos para este componente, si es necesario */
</style>
