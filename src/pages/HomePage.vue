<template>
  <!-- SideBar -->
  <SideBarOrganism />

  <!-- Map -->
  <div class="p-0 sm:ml-64">
    <MapOrganism />
  </div>
  
</template>

<script setup>
import SideBarOrganism from '@/components/organisms/SideBarOrganism.vue';
import MapOrganism from '@/components/organisms/MapOrganism.vue';
</script>
