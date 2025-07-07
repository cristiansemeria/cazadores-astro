<script setup>
import { reactive, ref } from 'vue';

// Estado del formulario
const form = reactive({
  name: '',
  email: '',
  service: '',
  message: '',
});

// Control del modal
const showModal = ref(false);
function openModal() {
  showModal.value = true;
}
function closeModal() {
  showModal.value = false;
}

// Manejo del envío
function handleSubmit() {
  console.log('Formulario enviado:', form);
  alert(`Gracias, ${form.name}. Hemos recibido tu solicitud.`);
  // Reseteo de campos
  form.name = '';
  form.email = '';
  form.service = '';
  form.message = '';
  // Cerrar modal
  closeModal();
}
</script>

<template>
  <div>
    <!-- Botón para abrir el formulario -->
    <button
        @click="openModal"
        class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
    >
      Abrir Formulario
    </button>

    <!-- Modal emergente -->
    <div
        v-if="showModal"
        class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50"
    >
      <div class="bg-white rounded-lg shadow-lg max-w-md w-full mx-4 p-6 relative">
        <!-- Botón de cerrar -->
        <button
            @click="closeModal"
            class="absolute top-3 right-3 text-gray-500 hover:text-gray-700 text-xl font-bold"
        >
          &times;
        </button>

        <form @submit.prevent="handleSubmit" class="space-y-4">
          <div>
            <label for="name" class="block text-sm font-medium text-gray-700">Nombre</label>
            <input
                id="name"
                v-model="form.name"
                type="text"
                required
                class="mt-1 w-full border border-gray-300 rounded p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
          </div>

          <div>
            <label for="email" class="block text-sm font-medium text-gray-700">Correo electrónico</label>
            <input
                id="email"
                v-model="form.email"
                type="email"
                required
                class="mt-1 w-full border border-gray-300 rounded p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
          </div>

          <div>
            <label for="service" class="block text-sm font-medium text-gray-700">Servicio</label>
            <select
                id="service"
                v-model="form.service"
                required
                class="mt-1 w-full border border-gray-300 rounded p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
              <option value="" disabled>Seleccione un servicio</option>
              <option value="consultoria">Consultoría</option>
              <option value="desarrollo">Desarrollo</option>
              <option value="soporte">Soporte</option>
            </select>
          </div>

          <div>
            <label for="message" class="block text-sm font-medium text-gray-700">Mensaje</label>
            <textarea
                id="message"
                v-model="form.message"
                rows="4"
                class="mt-1 w-full border border-gray-300 rounded p-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            ></textarea>
          </div>

          <button
              type="submit"
              class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
          >
            Enviar
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>