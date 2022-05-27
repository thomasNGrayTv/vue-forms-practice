<script setup>
const props = defineProps({
  label: {
    type: String,
    default: "",
  },
  modelValue: {
    type: [String, Number],
    default: "",
  },
  value: {
    type: [String, Number],
    required: true,
  },
});

const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <input
    type="radio"
    :checked="props.modelValue === props.value"
    :value="props.value"
    @change="emit('update:modelValue', props.value)"
    v-bind="$attrs"
  />
  <label v-if="props.label">{{ props.label }}</label>
</template>

<style></style>
