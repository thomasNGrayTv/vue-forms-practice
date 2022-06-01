<script setup>
import { ref } from "vue";
import BaseInput from "../components/BaseInput.vue";
import BaseSelect from "../components/BaseSelect.vue";
import BaseCheckbox from "../components/BaseCheckbox.vue";
import BaseRadioGroup from "../components/BaseRadioGroup.vue";
import axios from "axios";
import { useField, useForm } from "vee-validate";
import { required, minLength, anything } from "../features/ValidationRules";

const validationSchema = {
  category: required,
  title: (value) => {
    const req = required(value);
    const min = minLength(3, value);

    if (!req) {
      return req;
    }

    if (!min) {
      return min;
    }

    return true;
  },
  description: required,
  location: undefined,
  pets: anything,
  catering: anything,
  music: anything,
};

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

let sendError = ref(null);

const { handleSubmit } = useForm({
  validationSchema,
});

const { value: category, errorMessage: categoryError } = useField("category");
const { value: title, errorMessage: titleError } = useField("title");
const { value: description, errorMessage: descriptionError } =
  useField("description");
const { value: location, errorMessage: locationError } = useField("location");
const { value: pets, errorMessage: petsError } = useField("pets", undefined, {
  initialValue: 1,
});
const { value: catering, errorMessage: cateringError } = useField(
  "catering",
  undefined,
  { initialValue: false }
);
const { value: music, errorMessage: musicError } = useField(
  "music",
  undefined,
  { initialValue: false }
);

function sendForm() {
  axios
    .post(
      "https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events",
      event.value
    )
    .then((response) => {
      console.log("response: ", response);
    })
    .catch((err) => {
      console.log("error", err);
      sendError.value = err;
    });
}
</script>

<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <BaseSelect
        v-model="category"
        :error="categoryError"
        :options="categories"
        label="Select a category"
      ></BaseSelect>

      <fieldset>
        <legend>Name & describe your event</legend>
        <BaseInput
          v-model="title"
          :error="titleError"
          label="Title"
          type="text"
        ></BaseInput>
        <BaseInput
          v-model="event.description"
          label="Description"
          type="text"
        ></BaseInput>
      </fieldset>

      <fieldset>
        <legend>Where is your event?</legend>
        <BaseInput
          v-model="location"
          :error="locationError"
          label="Location"
          type="text"
        ></BaseInput>
      </fieldset>

      <fieldset>
        <legend>Pets</legend>
        <p>Are pets allowed?</p>
        <div>
          <BaseRadioGroup
            v-model="pets"
            :error="petsError"
            name="pets"
            :options="petOptions"
            vertical
          ></BaseRadioGroup>
        </div>
      </fieldset>

      <fieldset>
        <legend>Extras</legend>
        <div>
          <BaseCheckbox
            type="checkbox"
            label="Catering"
            v-model="catering"
            :error="cateringError"
          ></BaseCheckbox>
        </div>

        <div>
          <BaseCheckbox
            type="checkbox"
            label="Live Music"
            v-model="music"
            :error="musicError"
          ></BaseCheckbox>
        </div>
      </fieldset>

      <button type="submit">Submit</button>
      <p v-if="sendError" class="errorMessage">
        {{ sendError }}
      </p>
    </form>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}

fieldset {
  border: 0;
  margin: 0;
  padding: 0;
}

legend {
  font-size: 2em;
  font-weight: 700;
  margin-top: 20px;
}

.errorMessage {
  color: crimson;
}
</style>
