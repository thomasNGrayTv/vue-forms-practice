<script setup>
import { ref } from "vue";
import BaseInput from "../components/BaseInput.vue";
import BaseSelect from "../components/BaseSelect.vue";
import BaseCheckbox from "../components/BaseCheckbox.vue";
import BaseRadioGroup from "../components/BaseRadioGroup.vue";

const categories = ref([
  "sustainability",
  "nature",
  "animal welfare",
  "housing",
  "education",
  "food",
  "community",
]);
const event = ref({
  category: "",
  title: "",
  description: "",
  location: "",
  pets: 1,
  extras: {
    catering: false,
    music: false,
  },
});

const petOptions = ref([
  {
    label: "Yes",
    value: 1,
  },
  {
    label: "No",
    value: 0,
  },
]);
</script>

<template>
  <div>
    <h1>Create an event</h1>
    <form>
      <BaseSelect
        v-model="event.category"
        :options="categories"
        label="Select a category"
      ></BaseSelect>

      <h3>Name & describe your event</h3>

      <BaseInput v-model="event.title" label="Title" type="text"></BaseInput>
      <BaseInput
        v-model="event.description"
        label="Description"
        type="text"
      ></BaseInput>

      <h3>Where is your event?</h3>

      <BaseInput
        v-model="event.location"
        label="Location"
        type="text"
      ></BaseInput>

      <h3>Are pets allowed?</h3>
      <div>
        <BaseRadioGroup
          v-model="event.pets"
          name="pets"
          :options="petOptions"
        ></BaseRadioGroup>
      </div>

      <h3>Extras</h3>
      <div>
        <BaseCheckbox
          type="checkbox"
          label="Catering"
          v-model="event.extras.catering"
        ></BaseCheckbox>
      </div>

      <div>
        <BaseCheckbox
          type="checkbox"
          label="Live Music"
          v-model="event.extras.music"
        ></BaseCheckbox>
      </div>

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
