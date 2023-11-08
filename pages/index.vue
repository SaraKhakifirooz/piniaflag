<template>
    <div class="w-[100%] m-auto bg-gray-100">
        <div class="flex bg-green-200 p-3 mb-2 justify-between">
            <h1 class="bg-green-500 p-2">
                <nuxt-link to="/">Home</nuxt-link>
            </h1>
            <h1 class="bg-green-100 p-2">
                <nuxt-link to="/favorites">Favorite</nuxt-link>
            </h1>
        </div>
        <br>
        <div class="w-[100%] m-auto">
            <ul class="flex flex-wrap justify-center">
                <li v-for="(country, i ) in result" :key="i" class="w-[20%] bg-white m-3 p-2">
                    <!-- --------------------- -->
                    <img :src="country.flags.svg" :alt="country.name.common" class="w-full h-[100px]" />
                    {{ country.name.common }}

                    <button v-if="countryStore.isFavorite(country)" @click="toggleFavorite(country)"
                        class="bg-red-100 flex text-xs items-center p-2 rounded-2xl">
                        <svg fill="#000" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
                            <path
                                d="M12 4.419c-2.826-5.695-11.999-4.064-11.999 3.27 0 7.27 9.903 10.938 11.999 15.311 2.096-4.373 12-8.041 12-15.311 0-7.327-9.17-8.972-12-3.27z" />
                        </svg>
                        Disfavorite
                    </button>

                    <button v-if="!countryStore.isFavorite(country)" @click="toggleFavorite(country)"
                        class="bg-green-500 flex text-xs items-center p-2 rounded-2xl">
                        <svg fill="red" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
                            <path
                                d="M12 4.419c-2.826-5.695-11.999-4.064-11.999 3.27 0 7.27 9.903 10.938 11.999 15.311 2.096-4.373 12-8.041 12-15.311 0-7.327-9.17-8.972-12-3.27z" />
                        </svg>
                        Favorites
                    </button>


                    <!-- --------------------- 
                      / این مشکلش چیه ؟؟ کار نمیکنه ؟؟  //TODO

                                <button @click="pushHeart(item)">
                                    {{ alreadyInCart(item) ? 'In Cart' : 'Add to cart' }}
                                </button>
                         
                    </div> -->

                </li>
            </ul>
        </div>

    </div>
</template>

<script setup>

const result = await $fetch('https://restcountries.com/v3.1/all').catch((error) => error.data)


// این مشکلش چیه ؟؟ کار نمیکنه ؟؟  //TODO
// const alreadyInCart = (item) => {
//     debugger;
//     const x = flagfav.cartfav?.find(el => el.id === item.id)
//     if (x?.id) {
//         return true
//     } else {
//         return false
//     }
// }


import { useFlagStore } from "~/stores/FlagStore";

const countryStore = useFlagStore();

const toggleFavorite = (country) => {
    if (countryStore.isFavorite(country)) {
        countryStore.removeFromFavorites(country);
    } else {
        countryStore.addToFavorites(country);
    }
};


</script>
