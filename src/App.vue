<script setup lang="ts">
import FolderIcon from "./components/icons/FolderIcon.vue";
import FileIcon from "./components/icons/FileIcon.vue";
import AddFolderButton from "./components/AddFolderButton.vue";

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
          }
        ]
      }
    ],
  },
  {
    "id": "7",
    "type": "file",
    "name": "public.js",
    "created_at": "2021-06-01 12:00:00",
    "updated_at": "2021-06-01 21:30:00"
  }
];
</script>

<template>
  <div>
    <div class="h-screen overflow-hidden bg-amber-100">
      <div class="flex">
        <div class="bg-zinc-800 h-screen w-[360px] p-3.5">
          <ul class="list-none text-white">
            <li v-for="node in initialTree" :key="node.id">
              <ul v-if="node?.type === 'folder'">
                <li class="cursor-pointer">
                  <div class="flex justify-between gap-1.5">
                    <div class="flex gap-1.5">
                      <FolderIcon/>
                      <span>{{ node.name }}</span>
                    </div>
                    <AddFolderButton />
                  </div>
                  <ul v-if="node.hasOwnProperty('children') && node.children.length > 0" class="ml-2">
                    <li class="cursor-pointer">
                      <ul class="list-none">
                        <li v-for="child in node.children">
                          <ul v-if="child.type === 'folder'">
                            <li>
                              <div class="flex justify-between gap-1.5">
                                <div class="flex gap-1.5">
                                  <FolderIcon/>
                                  <span>{{ node.name }}</span>
                                </div>
                                <AddFolderButton />
                              </div>
                            </li>
                          </ul>
                          <div v-if="child.type === 'file'">
                            <div class="flex gap-1.5">
                              <FileIcon/>
                              <span>{{ child.name }}</span>
                            </div>
                          </div>
                        </li>
                      </ul>
                    </li>
                  </ul>
                </li>
              </ul>
              <ul v-if="node?.type === 'file'">
                <li>
                  <div class="flex gap-1.5">
                    <FileIcon />
                    <span>{{ node.name }}</span>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <div class="bg-amber-200 w-full"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
