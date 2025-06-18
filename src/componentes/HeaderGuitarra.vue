import { DatosGuitarra } from '../interfaces/DatosGuitarra';
<template>
  <header class="py-5 header">
    <div class="container-xl">
      <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
          <a href="index.html">
            <img class="img-fluid" src="/img/logo.svg" alt="imagen logo" />
          </a>
        </div>
        <nav class="col-md-6 a mt-5 d-flex align-items-start justify-content-end">
          <div class="carrito">
            <img class="img-fluid" src="/img/carrito.png" alt="imagen carrito" />

            <div id="carrito" class="bg-white p-3">
              <p v-if="carrito.length === 0" class="text-center">El carrito esta vacio</p>
              <div v-else>
                <table class="w-100 table">
                  <thead>
                    <tr>
                      <th>Imagen</th>
                      <th>Nombre</th>
                      <th>Precio</th>
                      <th>Cantidad</th>
                      <th></th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="guitar in guitarP" :key="guitar.id">
                      <td>
                        <img
                          class="img-fluid"
                          :src="'/img/' + guitar.imagen + '.jpg'"
                          alt="imagen guitarra"
                        />
                      </td>
                      <td>{{ guitar.nombre }}</td>
                      <td class="fw-bold">${{ guitar.precio }}</td>
                      <td class="flex align-items-start gap-4">
                        <button
                          type="button"
                          class="btn btn-dark"
                          @click="$emit('decrementar-cantidad', guitar.id)"
                        >
                          -
                        </button>
                        {{ guitar.cantidad }}
                        <button
                          type="button"
                          class="btn btn-dark"
                          @click="$emit('incrementar-cantidad', guitar.id)"
                        >
                          +
                        </button>
                      </td>
                      <td>
                        <button
                          class="btn btn-danger"
                          type="button"
                          @click="$emit('eliminar-guitarra', guitar.id)"
                        >
                          X
                        </button>
                      </td>
                    </tr>
                  </tbody>
                </table>

                <p class="text-end">
                  Total pagar: <span class="fw-bold">${{ totalPagar }}</span>
                </p>
                <button class="btn btn-dark w-100 mt-3 p-2">Vaciar Carrito</button>
              </div>
            </div>
          </div>
        </nav>
      </div>
      <!--.row-->

      <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
          <h1 class="display-2 fw-bold">Modelo {{ guitarraPrincipal.nombre }}</h1>
          <p class="mt-5 fs-5 text-white">
            {{ guitarraPrincipal.descripcion }}
          </p>
          <p class="text-primary fs-1 fw-black">${{ guitarraPrincipal.precio }}</p>
          <button type="button" class="btn fs-4 bg-primary text-white py-2 px-5">
            Agregar al Carrito
          </button>
        </div>
      </div>
    </div>

    <img class="header-guitarra" src="/img/header_guitarra.png" alt="imagen header" />
  </header>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps({
  carrito: {
    type: Array,
    required: true,
  },
  guitarraPrincipal: {
    type: Object,
    required: true,
  },
});

interface carritos {
  id: number;
  nombre: string;
  precio: number;
  imagen: string;
  descripcion: string;
  cantidad: number;
}
const carrit = <carritos[]>props.carrito;
const guitarP = <carritos[]>props.guitarraPrincipal;
defineEmits(['incrementar-cantidad', 'decrementar-cantidad', 'eliminar-guitarra']);

const totalPagar = computed(() => {
  return carrit.reduce((total: number, carrit) => total + carrit.cantidad * carrit.precio, 0);
});
</script>

<style scoped></style>
