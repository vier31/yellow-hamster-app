<script setup lang="ts">
import { Drawer, DrawerContent } from "@progress/kendo-vue-layout";
import { useRouter } from "vue-router";
import { computed, ref, onActivated } from "vue";
import { useLocalStorage } from "@vueuse/core";

const router = useRouter();
const currentRoute = computed(() => router.currentRoute.value);

const expanded = useLocalStorage("drawer-expanded", true);
const expandedIcon = computed(() => {
  return expanded.value ? "k-i-arrow-chevron-left" : "k-i-arrow-chevron-right";
});

const items = computed(() => [
  {
    text: "Boards",
    icon: "k-i-set-column-position",
    selected: true,
    data: {
      path: "/",
    },
  },
  {
    text: "Templates",
    icon: "k-i-border-left",
    data: {
      path: "/templates",
    },
  },
  {
    text: "Settings",
    icon: "k-i-gear",
    data: {
      path: "/settings",
    },
  },
  {
    text: "Collapse",
    icon: expandedIcon.value,
    data: {
      action: () => (expanded.value = !expanded.value),
    },
  },
]);

const getIndexFromPath = computed(() => {
  return items.value.findIndex((item) => {
    return item.text.toLowerCase() === currentRoute.value.name;
  });
});
const selectedId = ref(getIndexFromPath);

function onSelect({ itemIndex }: { itemIndex: number }) {
  const item = items.value[itemIndex];

  if (item.data.path) {
    router.push(item.data.path);
  }
  if (typeof item.data.action === "function") item.data.action();
}
</script>

<template>
  <Drawer
    class="h-[100vh]"
    :expanded="expanded"
    position="start"
    mode="push"
    :mini="true"
    :items="
      items.map((item, index) => ({
        ...item,
        selected: index === selectedId,
      }))
    "
    @select="onSelect"
  >
    <DrawerContent>
      <div class="px-5">
        <router-view />
      </div>
    </DrawerContent>
  </Drawer>
</template>
