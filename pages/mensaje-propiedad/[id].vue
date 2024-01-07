<template>
  <!-- component -->
  <div class="min-h-screen p-6 bg-gray-100 flex items-center justify-center">
    <div class="container max-w-screen-lg mx-auto">
      <div>
        <h2 class="font-semibold text-xl text-gray-600">
          Contacto a {{ itemData.name }}
        </h2>
        <p class="text-gray-500 mb-6">
          Envianos aca tu mensaje te responderemos pronto
        </p>

        <div class="bg-white rounded shadow-lg p-4 px-4 md:p-8 mb-6">
          <div class="grid gap-4 gap-y-2 text-sm grid-cols-1 lg:grid-cols-3">
            <div class="text-gray-600">
              <p class="font-medium text-lg">Mensaje</p>
            </div>

            <div class="lg:col-span-2">
              <div
                class="grid gap-4 gap-y-2 text-sm grid-cols-1 md:grid-cols-5"
              >
                <div class="md:col-span-5">
                  <label for="full_name">Titulo</label>
                  <input
                    type="text"
                    class="h-10 border mt-1 rounded px-4 w-full bg-gray-50"
                    v-model="title"
                  />
                </div>
                <div class="md:col-span-5">
                  <label for="full_name">Mensaje</label>
                  <textarea
                    type="text"
                    class="border mt-1 rounded px-4 w-full bg-gray-50"
                    rows="10"
                    v-model="content"
                  ></textarea>
                </div>

                <div class="md:col-span-5 text-right">
                  <div class="inline-flex items-end">
                    <button
                      @click="mensaje()"
                      class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                    >
                      Enviar
                    </button>
                  </div>
                </div>
              </div>
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
  console.log("no tiene sesion");
}
const route = useRoute();

const itemData = await $fetch(
  `http://localhost:4000/api/properties/${route.params.id}`
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
    .post("http://localhost:4000/api/messages", playload, { headers })
    .then((result) => {
      if (result.data.status == 200) {
        router.push("/admin/");
      }
    });
};
</script>