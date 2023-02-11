<script lang="ts" setup>
import EyeSlashed from "~icons/akar-icons/eye-slashed";
import EyeOpen from "~icons/akar-icons/eye-open";

const showPassword = ref(false);

const props = defineProps<{
  disabled?: boolean;
  name?: string;
  id?: string;
  placeholder?: string;
  modelValue: string;
}>();

const emit = defineEmits<{
  (e: "update:modelValue", value: string): void;
}>();

function onInput(value: string): void {
  emit("update:modelValue", value);
}

watch(
  () => props.disabled,
  (val) => {
    if (val) showPassword.value = false;
  }
);
</script>
<template>
  <div class="mb-4 inline-flex items-stretch rounded focus-within:ring">
    <VInput
      :modelValue="modelValue"
      @update:model-value="onInput"
      required
      class="mb-0 rounded-r-none text-slate-900 focus:ring-0"
      :name="name"
      :id="id"
      :placeholder="placeholder"
      :disabled="disabled"
      :type="showPassword ? 'text' : 'password'"
    />
  </div>
</template>
