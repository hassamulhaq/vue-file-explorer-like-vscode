<script setup lang="ts">

import FileIcon from "./icons/FileIcon.vue";

type nodeType = {
  id: string;
  type: string;
  name: string;
  created_at: string;
  updated_at: string;
};

const props = defineProps({
  node: {
    type: Object as PropType<nodeType>,
    required: true,
  },
});

const emit = defineEmits(['fileClicked']);

</script>

<template>
  <ul class="text-white">
    <li class="fileBlock cursor-pointer py-0.5 px-1.5 rounded hover:bg-zinc-700">
      <div class="flex gap-1.5">
        <FileIcon />
        <span @click="(event) => emit('fileClicked', props.node)">{{ props.node.name }}</span>
      </div>
    </li>
  </ul>
</template>

<style scoped>

</style>