<script setup lang="ts">
const props = defineProps<{
  label: string
}>()
</script>

<template>
  <span class="ms-3">{{ props.label }}</span>
</template>