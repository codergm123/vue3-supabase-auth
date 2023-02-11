<script lang="ts" setup>
import LoadingIcon from "~icons/ant-design/loading-outlined";
defineProps<{
  loading?: boolean;
}>();
</script>
<template>
  <button class="widgetbutton mb-4 w-full rounded py-2 text-sm text-slate-50">
    <slot v-if="!loading" />
    <LoadingIcon v-else class="mx-auto h-5 animate-spin" data-cy="loading" />
  </button>
</template>

<style>
.widgetbutton {
  margin-top: 24px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 8px 10px;
  gap: 4px;

  width: 400px;
  height: 40px;

  /* Primary */

  background: #322DF0;
  box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.12), 0px 0px 12px rgba(0, 0, 0, 0.04);
  border-radius: 4px;
}
</style>