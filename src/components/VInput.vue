<script lang="ts" setup>
defineProps<{
  modelValue: string;
}>();

const emit = defineEmits<{
  (e: "update:modelValue", value: string): void;
}>();

function onInput(event: Event): void {
  const target = event.target as HTMLInputElement;
  emit("update:modelValue", target.value);
}
</script>
<template>
  <input
    :value="modelValue"
    @input="onInput"
    class="widgetinput outline-none transition focus:ring"
  />
</template>

<style>
.widgetinput {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 8px 12px;

  width: 400px;
  height: 40px;

  background: #FFFFFF;
  border: 2px solid rgba(0, 0, 0, 0.24);
  border-radius: 4px;
}
</style>