<script setup lang="ts">
import Folder from "./components/Folder.vue";
import File from "./components/File.vue";
import AddIcon from "./components/icons/AddIcon.vue";
import Input from "./components/Input.vue";
import {ref} from "vue";

const initialTree = [
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
];

const fileClicked = (e) => {
  console.log(e);
};

const showInput = ref(false);
const inputValue = ref('');

</script>

<template>
  <div>
    <div class="h-screen overflow-hidden bg-amber-100">
      <div class="flex">
        <div class="bg-zinc-800 h-screen w-[360px] p-3.5">
          <div class="flex justify-end h-[26px]">
            <Input
                v-if="showInput"
                v-model="inputValue"
                node-id="0" />
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
