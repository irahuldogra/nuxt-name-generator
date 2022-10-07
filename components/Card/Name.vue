<script setup lang="ts">
interface Props {
  name: string;
  index: number;
}

const props = defineProps<Props>();

const emit = defineEmits(['remove']);

const removeName = () => {
  emit('remove', props.index);
};
</script>
<template>
  <div class="relative w-[32%] mb-4 mx-1 bg-purple-400 rounded-2xl p-1 py-8">
    <h4 class="font-medium text-md">{{ name }}</h4>
    <p
      class="absolute text-purple-800 font-bold top-[5%] left-[91%] cursor-pointer"
      @click="removeName"
    >
      X
    </p>
  </div>
</template>
