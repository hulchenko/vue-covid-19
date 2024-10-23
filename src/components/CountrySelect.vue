<script setup>
import { ref } from "vue";
import countries from "@/data/countries.json";

const selected = ref(0);
const emit = defineEmits(["changeCountry"]);
const { loading } = defineProps(["loading"]);

const onChange = (e) => {
  // loading.value = true; TODO
  console.log(`LOADING: `, loading);
  const selectedCountry = e.target.value;
  emit("changeCountry", selectedCountry);
};
</script>

<template>
  <select @change="onChange" v-model="selected" class="form-select block w-full border p-3 rounded mt-10">
    <option value="0">Select Country</option>
    <option v-for="country in countries" v-bind:value="country.name">{{ country.name }}</option>
  </select>
</template>
