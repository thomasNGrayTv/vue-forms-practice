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
  options: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["update:modelValue"]);
</script>

<template>
  <label v-if="props.label">{{ props.label }}</label>
  <select
    :value="props.modelValue"
    class="field"
    v-bind="{
      ...$attrs,
      onChange: ($event) => {
        emit('update:modelValue', $event.target.value);
      },
    }"
  >
    <option
      v-for="option in options"
      :value="option"
      :key="option"
      :selected="option === props.modelValue"
    >
      {{ option }}
    </option>
  </select>
</template>

<style></style>
