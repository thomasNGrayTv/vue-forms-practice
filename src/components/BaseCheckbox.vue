<script setup>
const props = defineProps({
  label: {
    type: String,
    default: "",
  },
  modelValue: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <input
    v-bind="$attrs"
    :checked="modelValue"
    class="field"
    @change="emit('update:modelValue', $event.target.checked)"
  />
  <label v-if="props.label">{{ props.label }}</label>
</template>

<style></style>
