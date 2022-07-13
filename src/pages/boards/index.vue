<script setup lang="ts">
import type { Board } from "@/types";
import { ref } from "vue";

const dummyBoards = ref<Partial<Board>[]>([
  {
    id: "1",
    title: "My First Board",
    order: "[]",
    image: {
      downloadUrl: "https://picsum.photos/480/270?board=1",
    },
  },
  {
    id: "2",
    title: "My Second Board",
    order: "[]",
    image: {
      downloadUrl: "https://picsum.photos/480/270?board=2",
    },
  },
  {
    id: "3",
    title: "My Third Board",
    order: "[]",
  },
]);
</script>

<template>
  <h1 class="text-xl">Boards</h1>

  <ul class="flex flex-col items-center">
    <template v-for="board in dummyBoards" :key="board.id">
      <router-link :to="`/boards/${board.id}`" class="block w-96">
        <li class="border border-solid border-gray-200 rounded mt-2">
          <h3 class="text-lg">{{ board.title }}</h3>
          <img :src="board.image?.downloadUrl" />
        </li>
      </router-link>
    </template>
    <button class="border-solid border border-gray-200 p-2 mt-6">
      + Create new board
    </button>
  </ul>
</template>
