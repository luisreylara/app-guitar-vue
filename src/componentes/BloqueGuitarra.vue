<template>
  <div class="col-md-6 col-lg-4 my-4 row align-items-center">
    <div class="col-4">
      <img
        class="img-fluid"
        v-bind:src="'/img/' + guitarra.imagen + '.jpg'"
        v-bind:alt="'imagen guitarra: ' + guitarra.nombre"
      />
    </div>
    <div class="col-8">
      <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitarra.nombre }}</h3>
      <p>
        {{ guitarra.descripcion }}
      </p>
      <p class="fw-black text-primary fs-3">${{ guitarra.precio }}</p>
      <button
        type="button"
        class="btn btn-dark w-100"
        @click="
          $emit('agregarCarrito', guitarra.id, guitarra.nombre, guitarra.precio, guitarra.imagen)
        "
      >
        Agregar al Carrito
      </button>
    </div>
  </div>
  <!-- FIN GUITARRA -->
</template>

<script setup lang="ts">
defineEmits<{
  agregarCarrito: [id: number, nombre: string, precio: number, imagen: string];
}>();

defineProps({
  guitarra: {
    type: Object,
    required: true,
  },
});
</script>
