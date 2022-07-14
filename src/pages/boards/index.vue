<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
	import type { Board } from "@/types";
	import { useAlerts } from "@/stores/alerts";
	import { ref } from "vue";
	import AppButtonVue from "@/components/AppButton.vue";

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

	const showVerticalOrHorizontal = ref("vertical");

	/* Alerts with Store Pinia */
	const alertApp = useAlerts();
	function createBoard() {
		// console.log("board created");
		alertApp.success("New board created successfully!");
	}
</script>

<template>
	<h1 class="text-xl mb-5">Boards</h1>
	<section id="presentation_board">
		<AppButtonVue
			:togglable="true"
			:disabled="showVerticalOrHorizontal === 'vertical'"
			@click="showVerticalOrHorizontal = 'vertical'"
		>
			vertical
		</AppButtonVue>
		<AppButtonVue
			:togglable="true"
			:disabled="showVerticalOrHorizontal === 'horizontal'"
			@click="showVerticalOrHorizontal = 'horizontal'"
		>
			horizontal
		</AppButtonVue>
	</section>
	<div
		class="flex"
		:class="
			showVerticalOrHorizontal === 'vertical' ? 'flex-col items-center' : ''
		"
	>
		<BoardCard v-for="board in dummyBoards" :key="board.id" :board="board" />
		<AppButtonVue
			:theme-color="'secondary'"
			class="border-solid border border-gray-200 p-2 mt-6"
			@click="createBoard()"
		>
			+ Create new board
		</AppButtonVue>
	</div>
</template>

<!-- TODO: present error render app line 50 (image) -->
<!-- <template>
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
    <AppButtonVue class="border-solid border border-gray-200 p-2 mt-6">
      + Create new board
    </AppButtonVue>
  </ul>
</template> -->

<style scoped></style>
