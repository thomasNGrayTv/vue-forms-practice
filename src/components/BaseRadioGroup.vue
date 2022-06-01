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
  vertical: {
    type: Boolean,
    default: false,
  },
});
const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <component
    v-for="(option, index) in props.options"
    :key="index"
    :is="vertical ? 'div' : 'span'"
    :class="{
      horizontal: !vertical,
    }"
  >
    <BaseRadio
      :value="option.value"
      :label="option.label"
      :name="props.name"
      :modelValue="modelValue"
      @update:modelValue="emit('update:modelValue', $event)"
    ></BaseRadio>
  </component>
</template>

<style>
.horizontal {
  margin: 0em 0.51em;
}
</style>
