<script setup>
  import {productos} from "./datos";
  import {computed, ref} from "vue";

  const contador = ref(0);
  const total = productos.length;

  const siguiente = () => {
    contador.value ++;
    if (contador.value == total) {
      contador.value = 0;
    }
  }

  const anterior = () => {
    console.log(contador.value);
    if (contador.value == 0) {
      contador.value = total-1;
    } else {
      contador.value --;
    }
  }

  const rey = computed(() => {
    const nombre =  productos[contador.value].nombre.toLocaleLowerCase();
    return nombre.substring(0,1).toUpperCase() + nombre.substring(1);
  });

  const imagen = computed(() => {
    return `https://www.html6.es/img/rey_${productos[contador.value].nombre.toLowerCase()}.png`;
  });

  const descuento = computed(() => {
    const precio = productos[contador.value].precio - productos[contador.value].precio * 0.1;
    return Number(precio).toFixed(2);
  })

</script>

<template>
  <div class="grid h-screen place-items-center">
    <div class="flex flex-col items-center space-y-5 m-10 p-8 bg-gray-50 rounded-lg border-2 border-gray-400 shadow-xl">
      <h2 class="text-4xl font-bold">Cena {{ contador + 1 }} con el rey godo <span class="text-green-600">{{ rey }}</span></h2>
      <h3 class=" text-2xl font-bold">Precio: <span class="text-green-600">{{ productos[contador].precio }} $</span></h3>
      <div class="">
        <span v-if="productos[contador].finDeSemana" class="px-6 py-3 bg-red-600 text-white font-bold text-lg rounded-lg">(Solo fines de semana)</span>
        <span v-else class="px-6 py-3 bg-green-600 text-white font-bold text-lg rounded-lg">(De luneas a domingo)</span>
      </div>
      <p v-if="productos[contador].precio < 100" class="text-lg font-semibold">
        Ahora un 10% dto: <span class="text-green-600 font-bold">{{ descuento }}$</span> <img src="./assets/oferta.jpg" alt="" class="w-16 inline">
      </p>
      <img :src="imagen" :alt="productos[contador].nombre" class="h-96">
      <div class="flex flex-row space-x-4 items-center">
        <button @click="anterior()"  class="inline-flex items-center rounded border border-transparent bg-indigo-600 px-2.5 py-1.5 text-lg font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">&lt; Anterior</button>
        <span class="font-bold">{{ contador + 1}} / {{ total }}</span>
        <button @click="siguiente()"  class="inline-flex items-center rounded border border-transparent bg-indigo-600 px-2.5 py-1.5 text-lg font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Siguiente &gt;</button>
      </div>
    </div>
  </div>
</template>