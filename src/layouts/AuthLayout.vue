<script lang="ts" setup>
import { breakpointsTailwind } from "@vueuse/core";

/* after navigation on small screens, close the nav drawer */
const breakpoints = useBreakpoints(breakpointsTailwind);
const lgAndLarger = breakpoints.greater("lg");
const open = ref(false);
const route = useRoute();
watch(route, () => {
  if (!lgAndLarger.value) open.value = false;
});

onMounted(() => {
  if (lgAndLarger.value) open.value = true;
});
</script>

<template>
  <div class="flex h-full w-full max-w-full transition-colors">
    <div class="flex h-full max-h-full w-full max-w-full flex-grow flex-col bg-zinc-100 text-zinc-900 transition-all dark:bg-zinc-900 dark:text-zinc-100">
      <router-view />
    </div>
  </div>
</template>
