<template>
  <HeaderGuitarra
    :carrito="carrito"
    :guitarraPrincipal="guitarraPrincipal"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @eliminar-guitarra="eliminarItemGuitarra"
  />
  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <BloqueGuitarra
        v-for="guitarra in guitarras"
        :key="guitarra.id"
        v-bind:guitarra="guitarra"
        @agregarCarrito="addCarrito"
      />
    </div>
  </main>
  <FooterGuitarra />
</template>

<script setup lang="ts">
import BloqueGuitarra from './componentes/BloqueGuitarra.vue';
import HeaderGuitarra from './componentes/HeaderGuitarra.vue';
import FooterGuitarra from './componentes/FooterGuitarra.vue';
import { db } from './data/guitarra.ts';

import type { DatosGuitarra } from './interfaces/DatosGuitarra.ts';

import { ref } from 'vue';

const guitarras = ref(db);

const guitarraPrincipal = ref({});
guitarraPrincipal.value = db[3];

const carrito = ref<DatosGuitarra[]>([]);

const addCarrito = (id: number, nombre: string, precio: number, imagen: string) => {
  const existeEnCarrito = carrito.value.findIndex((prod) => prod.id === id);
  console.log(existeEnCarrito);

  if (existeEnCarrito >= 0) {
    if (typeof carrito.value[existeEnCarrito].cantidad != 'undefined') {
      carrito.value[existeEnCarrito].cantidad++;
    }
  } else {
    carrito.value.push({
      id,
      nombre,
      precio,
      imagen,
      cantidad: 1,
    });
  }
};

const incrementarCantidad = (id: number) => {
  const index = carrito.value.findIndex((prod) => prod.id === id);
  if (typeof carrito.value[index].cantidad != 'undefined') {
    if (carrito.value[index].cantidad >= 5) return;
    carrito.value[index].cantidad++;
  }
};
const decrementarCantidad = (id: number) => {
  const index = carrito.value.findIndex((prod) => prod.id === id);
  if (typeof carrito.value[index].cantidad != 'undefined') {
    if (carrito.value[index].cantidad <= 1) return;
    carrito.value[index].cantidad--;
  }
};

const eliminarItemGuitarra = (id: number) => {
  carrito.value = carrito.value.filter((item) => item.id !== id);
};
</script>

<style scoped></style>
