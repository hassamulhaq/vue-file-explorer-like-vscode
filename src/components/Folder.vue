<script setup lang="ts">

import FolderIcon from "./icons/FolderIcon.vue";
import AddFolderButton from "./AddFolderButton.vue";
import File from "./File.vue";
import Input from "./Input.vue";
import {ref} from "vue";


type nodeType = {
  id: string;
  type: string;
  name: string;
  created_at: string;
  updated_at: string;
  children?: nodeType[];
};

const props = defineProps({
  node: {
    type: Object as PropType<nodeType>,
    required: true,
  },
});


const showInput = ref(false);
const inputValue = ref('');

const emit = defineEmits(['fileClicked']);

const fileClickedX = (e) => {
  console.log('fileClickedX', e);
  emit('fileClicked', e);
}

const handleInputValue = (obj) => {
  if (!obj.hasOwnProperty('id') && !obj.hasOwnProperty('value'))
    alert('Invalid input');

  const {id, value} = obj;
  let isValidValue = false;

  const isFileAlreadyExists = props.node.children.some(child => child.name === value);
  if (isFileAlreadyExists) {
    alert('File already exists');
    return;
  }

  if (value !== '' && value.includes('.')) {
    const newNode = {
      id: `${props.node.children.length + 1}`,
      type: 'file',
      name: value,
      created_at: new Date().toISOString(),
      updated_at: new Date().toISOString(),
    };
    props.node.children.push(newNode);
    isValidValue = true;
  } else if (value !== '') {
    const newNode = {
      id: `${props.node.children.length + 1}`,
      type: 'folder',
      name: value,
      created_at: new Date().toISOString(),
      updated_at: new Date().toISOString(),
      children: []
    };
    props.node.children.push(newNode);
    isValidValue = true;
  }

  if (isValidValue) {
    showInput.value = false;
    inputValue.value = '';
  }
}

</script>

<template>
  <ul class="text-white">
    <li class="parent-node">
      <div class="folderBlock cursor-pointer py-0.5 px-1.5 rounded hover:bg-zinc-700 flex grow items-center justify-between gap-1.5">
        <div class="w-full grow">
          <div class="flex justify-between grow">
            <div class="flex gap-1.5">
              <FolderIcon />
              <span>{{ props.node.name }}</span>
            </div>
            <AddFolderButton @click="showInput = !showInput" />
          </div>
          <Input
              v-if="showInput"
              v-model="inputValue"
              :model-value="inputValue"
              @handleInputValue="handleInputValue"
              :node-id="props.node.id" />
        </div>
      </div>
      <ul v-if="props.node.hasOwnProperty('children') && props.node.children.length > 0" class="ml-2">
        <li>
          <template v-for="child in props.node.children">
            <Folder :node="child" v-if="child.type === 'folder'" />
            <File @fileClicked="fileClickedX" :node="child" v-else-if="child.type === 'file'" />
          </template>
        </li>
      </ul>
    </li>
  </ul>
</template>

<style scoped>
button.addFolderButton {
  color: #ffffff;
  border: none;
  cursor: pointer;
  display: none;
}

.folderBlock:hover .addFolderButton {
  display: block;
}
</style>