<template>
  <div class="min-h-screen flex items-center justify-center">
    <div class="bg-white p-8 rounded-lg shadow-md w-full sm:w-96">
      <h1 class="text-2xl font-bold mb-6">Iniciar Sesión</h1>

      <!-- Formulario de inicio de sesión -->
      <form>
        <!-- Campos del formulario (por ejemplo, email y contraseña) -->
        <div class="mb-4">
          <label for="email" class="block text-gray-700 text-sm font-bold mb-2"
            >Correo Electrónico</label
          >
          <input
            type="email"
            id="email"
            name="email"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-500"
          />
        </div>

        <div class="mb-4">
          <label
            for="password"
            class="block text-gray-700 text-sm font-bold mb-2"
            >Contraseña</label
          >
          <input
            type="password"
            id="password"
            name="password"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-500"
          />
        </div>

        <!-- Botón de inicio de sesión -->
        <button
          type="submit"
          class="w-full bg-blue-500 text-white px-4 py-2 rounded-md"
        >
          Iniciar Sesión
        </button>
      </form>
    </div>
  </div>
</template>

<script setup></script>

<style scoped>
/* Agrega estilos adicionales si es necesario */
</style>
