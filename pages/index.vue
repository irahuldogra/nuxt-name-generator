<script setup lang="ts">
import {
  OptionsInterface,
  Section,
  Gender,
  Popularity,
  Length,
  names,
} from '@/data';

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

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames;
};

const sectionsData: Section[] = [
  {
    title: '1) Choose a gender',
    category: 'gender',
    buttons: [Gender.BOY, Gender.UNISEX, Gender.GIRL],
  },
  {
    title: "2) Choose the name's popularity",
    category: 'popularity',
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose name's length",
    category: 'length',
    buttons: [Length.SHORT, Length.ALL, Length.LONG],
  },
];
</script>

<template>
  <div class="container max-w-4xl mx-auto text-center">
    <h1 class="text-2xl font-bold text-white">Name Generator</h1>
    <p class="my-1 font-light text-white">
      Choose your options and click the "Find Names" button below
    </p>
    <div
      class="relative p-3 mx-2 md:mx-auto bg-gradient-to-r from-indigo-100 to-purple-300 rounded-3xl"
    >
      <Option
        v-for="section in sectionsData"
        :key="section.title"
        :section="section"
        :options="options"
      />
      <button
        class="text-white hover:bg-purple-800 font-medium text-sm px-10 md:px-20 py-2.5 mb-2 mt-4 outline-none bg-purple-600 rounded-2xl focus:bg-purple-700 focus:ring-4 focus:ring-purple-300"
        @click="computeSelectedNames"
      >
        Find Names
      </button>
    </div>
    <div class="flex flex-wrap mt-4 text-white justify-evenly">
      <CardName
        v-for="(name, index) in selectedNames"
        :key="name"
        :name="name"
        :index="index"
        @remove="() => removeName(index)"
      />
    </div>
  </div>
</template>
