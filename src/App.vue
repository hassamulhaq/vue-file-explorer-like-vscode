<script setup lang="ts">
import Folder from "./components/Folder.vue";
import File from "./components/File.vue";
import AddIcon from "./components/icons/AddIcon.vue";
import Input from "./components/Input.vue";
import {ref} from "vue";

const initialTree = ref([
  {
    "id": "1",
    "type": "folder",
    "name": "root",
    "created_at": "2021-06-01 12:00:00",
    "updated_at": "2021-06-01 21:30:00",
    "children": [
      {
        "id": "2",
        "type": "file",
        "name": "hassam.js",
        "created_at": "2021-06-01 12:00:00",
        "updated_at": "2021-06-01 15:32:00"
      },
      {
        "id": "3",
        "type": "file",
        "name": "nuxt.js",
        "created_at": "2021-06-01 12:00:00",
        "updated_at": "2021-06-01 21:30:00"
      },
      {
        "id": "4",
        "type": "folder",
        "name": "components",
        "created_at": "2021-06-01 12:00:00",
        "updated_at": "2021-06-01 21:30:00",
        "children": [
          {
            "id": "5",
            "type": "file",
            "name": "Header.js",
            "created_at": "2021-06-01 12:00:00",
            "updated_at": "2021-06-01 21:30:00"
          },
          {
            "id": "6",
            "type": "file",
            "name": "Footer.js",
            "created_at": "2021-06-01 12:00:00",
            "updated_at": "2021-06-01 21:30:00"
          },
          {
            "id": "7",
            "type": "file",
            "name": "Main.js",
            "created_at": "2021-06-01 12:00:00",
            "updated_at": "2021-06-01 21:30:00"
          },
          {
            "id": "8",
            "type": "folder",
            "name": "icons",
            "children": [],
            "created_at": "2021-06-01 12:00:00",
            "updated_at": "2021-06-01 21:30:00",
          }
        ]
      }
    ],
  },
  {
    "id": "9",
    "type": "file",
    "name": "public.js",
    "created_at": "2021-06-01 12:00:00",
    "updated_at": "2021-06-01 21:30:00"
  }
]);

const fileClicked = (e) => {
  console.log(e);
};

const showInput = ref(false);
const inputValue = ref('');

const handleInputValue = (e) => {
  const isFileAlreadyExists = initialTree.value.some(child => child.name === e.target.value);
  if (isFileAlreadyExists) {
    alert('File already exists');
    return;
  }
  let isValidValue = false;

  const lastChild = initialTree.value[initialTree.value.length - 1];
  const lastChildId = lastChild.id;

  if (e.target.value !== '' && e.target.value.includes('.')) {
    const newNode = {
      id: `${Number(lastChildId) + 1}`,
      type: 'file',
      name: e.target.value,
      created_at: new Date().toISOString(),
      updated_at: new Date().toISOString(),
    };
    initialTree.value.push(newNode);
    isValidValue = true;
  } else if (e.target.value !== '') {
    const newNode = {
      id: `${Number(lastChildId) + 1}`,
      type: 'folder',
      name: e.target.value,
      created_at: new Date().toISOString(),
      updated_at: new Date().toISOString(),
      children: []
    };
    initialTree.value.push(newNode);
    isValidValue = true;
  }

  if (isValidValue) {
    inputValue.value = '';
  }
};

</script>

<template>
  <div>
    <div class="h-screen overflow-hidden bg-amber-100">
      <div class="flex">
        <div class="bg-zinc-800 h-screen overflow-y-auto w-[360px] p-3.5">
          <div class="flex justify-end h-[26px]">
            <Input
                v-if="showInput"
                v-model="inputValue"
                node-id="0"
                @keydown.enter="handleInputValue"
            />
            <button @click="showInput = !showInput" class="text-white hover:text-green-500 bg-transparent">
              <AddIcon />
            </button>
          </div>
          <div v-for="node in initialTree" :key="node.id">
            <Folder :node="node" v-if="node.type === 'folder'" />
            <File @fileClicked="fileClicked" :node="node" v-if="node.type === 'file'" />
          </div>
        </div>
        <div class="bg-green-200 w-full"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
