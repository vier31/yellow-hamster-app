<script setup lang="ts">
	import type { Task } from "@/types";
	import { ref, toRefs } from "vue";
	import AppImgDropzone from "../../components/AppImgDropzone.vue";
	// import BoardDragAndDrop from "../../components/BoardDragAndDrop.vue";
	const props = defineProps({
		id: String,
	});
	const { id: boardId } = toRefs(props);

	// For test data Local

	// const boardLocal = ref<Partial<Board>>({ // failed
	// TODO: PENDING resolved ISSUE uncomment  <BoardDragAndDrop>ERROR</BoardDragAndDrop>
	// TODO: uncomment line 16 - 26 and test console (Guide repo Speaker: BIFERT  4b68b8688306999523312868effc997fb2394f24)
	/* const boardLocal = ref({
		id: boardId?.value || "1",
		title: "Let's have an amazing time at Vue.js forge!! 🍍",
		order: JSON.stringify([
			{ id: "1", title: "backlog 🌴", taskIds: ["1", "2"] },
		]),
	});
	const tasksLocal = ref<Partial<Task>[]>([
		{ id: "1", title: "Code like mad people!" },
		{ id: "2", title: "Push clean code" },
	]); */
</script>

<template>
	<AppImgDropzone></AppImgDropzone>
	<!-- TODO: PENDING resolved ISSUE uncomment  <BoardDragAndDrop>ERROR</BoardDragAndDrop> -->
	<!-- <BoardDragAndDrop
		:board="boardLocal"
		:tasks="tasksLocal"
		@update=""
	></BoardDragAndDrop> -->
</template>
