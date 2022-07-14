<script lang="ts" setup>
	import { storeToRefs } from "pinia";
	import { useAlerts } from "@/stores/alerts";

	/* UI KENDO  https://www.telerik.com/kendo-vue-ui/components/notification/get-started/ */
	import { Fade } from "@progress/kendo-vue-animation";
	import {
		Notification,
		NotificationGroup,
	} from "@progress/kendo-vue-notification";

	/* Store Pinia */
	const storeApp = useAlerts();
	const { remove } = storeApp;
	const { items } = storeToRefs(storeApp);
</script>

<template>
	<div class="z-10">
		<NotificationGroup
			:style="{
				right: '25px',
				bottom: '15px',
				alignItems: 'flex-start',
				flexWrap: 'wrap-reverse',
			}"
		>
			<Fade v-for="alert in items" :key="alert.id" appear>
				<Notification
					:type="{
						style: alert.style,
						icon: true,
					}"
					:closable="alert.closable"
					@close="remove(alert.id)"
				>
					<div v-if="alert.html" v-html="alert.message"></div>
					<span v-else>{{ alert.message }}</span>
				</Notification>
			</Fade>
		</NotificationGroup>
	</div>
</template>
