<script setup lang="ts">
import { Gender, Popularity, Length, names } from '@/data';

interface OptionsInterface {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionsInterface>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.ALL,
});

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });

  selectedNames.value = filteredNames.map((name) => name.name);
};

const selectedNames = ref<string[]>([]);
</script>

<template>
  <div class="container max-w-4xl mx-auto font-sans text-center text-black">
    <h1 class="text-2xl">Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div
      class="relative p-3 mx-auto bg-gradient-to-r from-indigo-100 to-purple-300 rounded-3xl"
    >
      <div>
        <h4 class="p-2 font-semibold text-md">1) Choose a gender</h4>
        <section>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 rounded-l-lg"
            :class="
              options.gender === Gender.BOY &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2"
            :class="
              options.gender === Gender.UNISEX &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 rounded-r-lg"
            :class="
              options.gender === Gender.GIRL &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </section>
      </div>
      <div>
        <h4 class="p-2 font-semibold text-md">
          2) Choose the name's popularity
        </h4>
        <div>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 rounded-l-lg"
            :class="
              options.popularity === Popularity.TRENDY &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 rounded-r-lg"
            :class="
              options.popularity === Popularity.UNIQUE &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div>
        <h4 class="p-2 font-semibold text-md">3) Choose name's length</h4>
        <div>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 rounded-l-lg"
            :class="
              options.length === Length.LONG &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.length = Length.LONG"
          >
            Long
          </button>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2"
            :class="
              options.length === Length.ALL &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.length = Length.ALL"
          >
            All
          </button>
          <button
            class="text-white bg-purple-700 hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 rounded-r-lg"
            :class="
              options.length === Length.SHORT &&
              'outline-none ring-4 ring-purple-300 bg-purple-600 mr-1'
            "
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>
      <button
        class="text-white hover:bg-purple-800 font-medium text-sm px-20 py-2.5 mb-2 mt-4 outline-none bg-purple-600 rounded-2xl focus:bg-purple-700 focus:ring-4 focus:ring-purple-300"
        @click="computeSelectedNames"
      >
        Find Names
      </button>
    </div>
    <div class="flex flex-wrap mt-4 justify-evenly">
      <div
        class="relative w-[32%] mb-4 mx-1 text-white bg-purple-400 rounded-2xl p-1 py-8"
        v-for="name in selectedNames"
        :key="name"
      >
        <h4 class="font-medium text-md">{{ name }}</h4>
        <p
          class="absolute text-purple-800 font-bold top-[5%] left-[91%] cursor-pointer"
        >
          X
        </p>
      </div>
    </div>
  </div>
</template>
