<script setup lang="ts">
import { Section, OptionsInterface } from '@/data';

interface Props {
  section: Section;
  options: OptionsInterface;
}

const { section, options } = defineProps<Props>();

const computeButtonClasses = (value: string, index: number): string => {
  const classNames = [];

  if (options[section.category] === value) {
    const active: string =
      'outline-none ring-4 ring-purple-300 bg-violet-600 mr-1';
    classNames.push(active);
  }

  if (index === 0) {
    const roundedLeft: string = 'rounded-l-lg';
    classNames.push(roundedLeft);
  }

  if (index === section.buttons.length - 1) {
    const roundedRight: string = 'rounded-r-lg';
    classNames.push(roundedRight);
  }

  return classNames.join(' ');
};
</script>

<template>
  <div aria-label="options" class="container mx-auto md:my-2">
    <h4 class="p-2 font-semibold text-md">{{ section.title }}</h4>
    <div class="mb-2 text-sm font-medium text-white">
      <button
        v-for="(value, index) in section.buttons"
        class="bg-purple-700 hover:bg-purple-800 px-10 md:px-20 py-2.5"
        :class="computeButtonClasses(value, index)"
        :key="value"
        @click="options[section.category] = value"
      >
        {{ value }}
      </button>
    </div>
  </div>
</template>
