<script setup>
import BaseRadio from "./BaseRadio.vue";
const props = defineProps({
  options: {
    type: Array,
    required: true,
  },
  name: {
    type: String,
    required: true,
  },
  modelValue: {
    type: [String, Number],
    required: true,
  },
});
const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <BaseRadio
    v-for="(option, index) in props.options"
    :key="index"
    :value="option.value"
    :label="option.label"
    :name="props.name"
    :modelValue="modelValue"
    @update:modelValue="emit('update:modelValue', $event)"
  ></BaseRadio>
</template>

<style></style>
