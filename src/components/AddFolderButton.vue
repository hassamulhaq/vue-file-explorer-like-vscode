<script setup lang="ts">

import AddIcon from "./icons/AddIcon.vue";
</script>

<template>
  <button class="bg-transparent" @click="alert('clicked')">
    <AddIcon />
  </button>
</template>

<style scoped>

</style>