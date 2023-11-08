<template>
  <div class="w-[100%] m-auto bg-gray-100">
    <div class="flex bg-green-200 p-3 mb-2 justify-between">
      <h1 class="bg-green-100 p-2">
        <nuxt-link to="/">Home</nuxt-link>
      </h1>
      <h1 class="bg-green-500 p-2">
        <nuxt-link to="/favorites">Favorite</nuxt-link>
      </h1>
    </div>
    <br>
    <div class="flex flex-wrap w-[90%] m-auto">
      <div class="w-full flex flex-wrap">
        <div v-for="country in favorites" :key="country.name.common" class="m-2 bg-gray-200 p-2">
          <div class="w-[300px] h-[150px]">
            <img :src="country.flags.svg" :alt="country.name.common" class="w-full h-full" />
          </div>
          {{ country.name.common }}
        </div>
      </div>

      <div class="font-bold w-full mt-5">
        <h2>Borders : </h2>
      </div>
      <div>
        <div class="flex flex-wrap">
          <div v-for="(item, i) in countryStore.fetchBorders" :key="i" class="w-[20%] bg-white m-3 p-2">
            <img :src="item.flags.svg" class="w-full h-[100px]" />
            {{ item.name.common }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";
import { useFlagStore } from "~/stores/FlagStore";

const countryStore = useFlagStore();

const favorites = computed(() => countryStore.favorites);

</script>
