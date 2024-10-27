<script setup lang="ts">

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
  },
  nodeId: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(['update:modelValue', 'handleInputValue']);

</script>

<template>
  <input
      type="text"
      :node-id="props.nodeId"
      :model-value="modelValue"
      :value="modelValue"
      @keydown.enter="(event => emit('handleInputValue', {'id': props.nodeId, 'value': event.target.value}))"
      @input="$emit('update:modelValue', $event.target.value)"
      class="w-full border border-zinc-600 px-1.5 text-zinc-500 rounded bg-transparent outline-0 focus-visible:ring-0" />
</template>

<style scoped>

</style>