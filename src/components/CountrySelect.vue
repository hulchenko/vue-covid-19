<script setup>
import { ref } from "vue";
import countries from "@/data/countries.json";

const { modelValue } = defineProps(["modelValue"]); // country
const emit = defineEmits(["changeCountry, updateLoading"]);
const selected = ref(modelValue);

const onChange = (e) => {
  emit("updateLoading", true);
  const selectedCountry = e.target.value;
  selected.value = selectedCountry;
  emit("changeCountry", selectedCountry);
};
</script>

<template>
  <select @change="onChange" v-model="selected" class="form-select block w-full border p-3 rounded mt-10">
    <option value="0">Select Country</option>
    <option v-for="country in countries" :key="country.name" :value="country.name">{{ country.name }}</option>
  </select>
</template>
