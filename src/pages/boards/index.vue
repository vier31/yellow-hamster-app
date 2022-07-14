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
		{
			id: "4",
			title: "My Quarter Board",
			order: "[]",
		},
		{
			id: "5",
			title: "My Some Board",
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

	/* Board draggable */
	const getCoolGradient = (index: number) => {
		let finalGradientString = "";
		switch (index) {
			case 1:
				finalGradientString = "from-orange-400 to-pink-500";
				break;
			case 2:
				finalGradientString = "from-green-400 to-blue-400";
				break;
			case 3:
				finalGradientString = "from-purple-400 to-blue-400";
				break;
			default:
				finalGradientString = "from-orange-400 to-yellow-300";
		}
		return finalGradientString;
	};
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
	<!-- TODO: next remove Old version Exercise 2 (simple show experience comparison) -->
	<!-- 	<div
		class="flex"
		:class="
			showVerticalOrHorizontal === 'vertical'
				? 'flex-col items-center'
				: 'flex-wrap gap-2'
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
	</div> -->
	<div
		class="flex"
		:class="
			showVerticalOrHorizontal === 'vertical'
				? 'flex-col items-center'
				: 'flex-wrap gap-2'
		"
	>
		<div
			v-for="(board, index) in dummyBoards"
			:key="board.id"
			:class="getCoolGradient(index)"
			class="border rounded-md bg-gradient-to-tr"
		>
			<BoardCard
				:board="board"
				class="transition duration-100 ease-in border rounded-md hover:-rotate-3"
			/>
		</div>
		<AppButtonVue
			class="border-solid border border-gray-200 p-2 mt-6"
			:theme-color="'secondary'"
			@click="createBoard()"
		>
			+ Create new board
		</AppButtonVue>
	</div>
</template>

<style scoped></style>
