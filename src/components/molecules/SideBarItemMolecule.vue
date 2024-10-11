<script setup lang="ts">
import IconAtom from '../atoms/IconAtom.vue';
import LabelAtom from '../atoms/LabelAtom.vue';

const props = defineProps<{
  d_path: string,
  label: string
}>()
</script>

<template>
  <a href="#" class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700 group">
    <IconAtom :d_path="props.d_path"/>
    <LabelAtom :label="props.label"/>
  </a>
</template>