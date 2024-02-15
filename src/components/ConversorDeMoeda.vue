<template>
  <div class="container mx-auto">
    <p
      class="mt-2 text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl py-12"
    >
      CONVERSOR DE MOEDAS
    </p>

    <div class="flex flex-row">
      <div class="basis-1/2">
        <label> de: </label>
        <label for="currency" class="sr-only">Currency</label>
        <select
          v-model="de_selected"
          id="currency"
          name="currency"
          class="h-full bg-transparent rounded-md border-0 py-0 pl-1 pr-1 mr-2 text-gray-500 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm"
        >
          <option value="BRL">Real</option>
          <option value="USD">Dólar</option>
          <option value="CAD">Dólar Canadense</option>
          <option value="EUR">Euro</option>
          <option value="BTC">BitCoin</option>
          <option value="JPY">Iene Japonês</option>
          <option value="XAU">Ouro</option>
          <option value="ARS">Peso Argentino</option>
          <option value="CUP">Peso Cubano</option>
        </select>
      </div>

      <div class="basis-1/2">
        <label> para: </label>
        <label for="convert" class="sr-only">Convert</label>
        <select
          v-model="para_selected"
          id="convert"
          name="convert"
          class="h-full bg-transparent rounded-md border-0 py-0 pl-1 pr-1 text-gray-500 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm"
        >
          <option value="BRL">Real</option>
          <option value="USD">Dólar</option>
          <option value="CAD">Dólar Canadense</option>
          <option value="EUR">Euro</option>
          <option value="BTC">BitCoin</option>
          <option value="JPY">Iene Japonês</option>
          <option value="XAU">Ouro</option>
          <option value="ARS">Peso Argentino</option>
          <option value="CUP">Peso Cubano</option>
        </select>
      </div>
    </div>
  </div>

  <div class="mt-4 flex flex-row">
    <div class="basis-1/2">
      <div
        class="mt-4 col-start-1 row-start-3 self-center sm:mt-0 sm:col-start-2 sm:row-start-2 sm:row-span-2 lg:mt-6 lg:col-start-1 lg:row-start-3 lg:row-end-4"
      >
        <div class="relative mt-2 rounded-md shadow-sm">
          <div
            class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3"
          >
            <span class="text-gray-500 sm:text-sm">$</span>
          </div>
          <input
            v-model="price"
            type="number"
            name="price"
            id="price"
            class="block w-full rounded-md border-0 py-1.5 pl-7 pr-2 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            v-bind:placeholder="0.0"
          />
        </div>
      </div>
    </div>
    <div class="basis-1/2 ml-2">
      <div
        class="mt-4 col-start-1 row-start-3 self-center sm:mt-0 sm:col-start-2 sm:row-start-2 sm:row-span-2 lg:mt-6 lg:col-start-1 lg:row-start-3 lg:row-end-4"
      >
        <div class="relative mt-2 rounded-md shadow-sm">
          <button
            type="button"
            v-on:click="getCotacao()"
            class="bg-indigo-600 text-white leading-6 font-medium py-1.5 px-8"
          >
            CONVERTER
          </button>
        </div>
      </div>
    </div>
  </div>

  <p
    class="mt-2 text-3xl font-bold tracking-tight text-gray-900 sm:text-3xl py-12"
  >
    {{ para_selected + " $ " }} {{ result }}
  </p>
</template>


<script setup>
import { ref } from "vue";

const de_selected = ref("");
const para_selected = ref("");
const price = ref("");
let result = ref("");

function getCotacao() {
  let de_para = de_selected.value + "-" + para_selected.value;
  const url = "https://economia.awesomeapi.com.br/json/last/" + de_para;

  fetch(url)
    .then((res) => {
      return res.json();
    })
    .then((json) => {
      let cotacao = json[de_selected.value + para_selected.value];
      console.log(cotacao.bid);
      result.value = (cotacao.bid * parseFloat(price.value))
        .toFixed(2)
        .toString();
      console.log(price);
    });
}
</script>

<style lang="scss" scoped>
</style>