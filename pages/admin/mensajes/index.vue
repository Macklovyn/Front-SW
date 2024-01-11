<template>
  <menuAdmin />

  <div class="flex justify-between mx-20 mt-5">
    <h1 class="font-bold text-2xl">Mensajes</h1>

    <hr />
  </div>
  <div class="block w-full overflow-x-auto mx-20 mt-3">
    <table class="items-center bg-transparent w-full border-collapse">
      <thead>
        <tr>
          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Propiedad
          </th>

          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Usuario
          </th>

          <th
            class="px-6 bg-blueGray-50 text-blueGray-500 align-middle border border-solid border-blueGray-100 py-3 text-xs uppercase border-l-0 border-r-0 whitespace-nowrap font-semibold text-left"
          >
            Estado
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
            {{ categoria.property.name }}
          </th>
          <th
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4 text-left text-blueGray-700"
          >
            {{ categoria.user.name }}
          </th>
          <th
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4 text-left text-blueGray-700"
          >
            {{ categoria.status }}
          </th>
          <td
            class="border-t-0 px-6 align-middle border-l-0 border-r-0 text-xs whitespace-nowrap p-4"
          >
            <button
              v-if="categoria.status == 'CREADO'"
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
              @click="mostrarCuadroDialogo(categoria.id, categoria.message)"
            >
              Responder
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
const idEdit = ref("");
const token = ref(localStorage.getItem("token"));
useHead({
  title: "Categorias",
});

const getCategorias = () => {
  axios.get("https://api-proyectsw.onrender.com/api/messages").then((result) => {
    console.log(result);
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
    .delete("https://api-proyectsw.onrender.com/api/messages/" + id, { headers })
    .then((result) => {
      getCategorias();
    });
};

const mostrarCuadroDialogo = async (id, mensaje) => {
  idEdit.value = id;
  const { value: userInput } = await Swal.fire({
    title: "Responde el mensaje",
    text: mensaje,
    input: "text",
    inputLabel: "Respuesta:",
    showCancelButton: true,
    inputValidator: (value) => {
      if (!value) {
        return "Por favor, ingrese un valor";
      }
    },
  });

  if (userInput) {
    // Llamada a la función con el valor ingresado
    ejecutarFuncionConValor(userInput);
  }
};

// Función que se ejecuta con el valor ingresado
const ejecutarFuncionConValor = (valor) => {
  const playload = {
    messageId: idEdit.value,
    response: valor,
  };

  const headers = {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token.value}`,
  };

  axios
    .post("https://api-proyectsw.onrender.com/api/message/response", playload, { headers })
    .then((result) => {
      getCategorias();
    });
};
</script>