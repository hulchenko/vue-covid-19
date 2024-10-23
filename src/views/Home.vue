<script setup>
import { ref, onMounted } from "vue";
const API_KEY = import.meta.env.VITE_API_KEY;

import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

const loading = ref(true);
const currCountry = ref("Canada");
const stats = ref({
  confirmed: 0,
  critical: 0,
  deaths: 0,
  lastUpdate: new Date(),
  recovered: 0,
});

const fetchCovidData = async (country = "Canada") => {
  try {
    const res = await fetch(`https://covid-19-data.p.rapidapi.com/country?name=${country}`, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        "x-rapidapi-key": API_KEY,
      },
    });
    const data = await res.json();

    if (Array.isArray(data)) {
      return data[0];
    }
    return null;
  } catch (error) {
    console.error("Error fetching data: ", error);
  }
};

const countryChangeHandler = async (country) => {
  const data = await fetchCovidData(country);
  stats.value = data;
  currCountry.value = country;
  loading.value = false;
};

// Lifecycle hook on init load
onMounted(async () => {
  const data = await fetchCovidData();
  stats.value = data;
  loading.value = false;
});
</script>

<template>
  <main v-if="!loading" class="mt-44">
    <DataTitle :stats="stats" />
    <DataBoxes :stats="stats" />
    <CountrySelect @changeCountry="countryChangeHandler" @updateLoading="loading = $event" v-model="currCountry" />
  </main>

  <div class="mt-44" v-else>
    <div class="animate-pulse text-center border-red-400">
      <h2 class="text-3xl font-bold">Loading...</h2>
      <div class="text-2xl mt-4 mb-10 text-white">.</div>
    </div>

    <div class="grid md:grid-cols-2 gap-4">
      <div class="shadow-md bg-indigo-50 p-10 h-44 text-center rounded">
        <div class="animate-pulse flex space-x-4">
          <div class="flex-1 space-y-12 py-1">
            <div class="h-3 bg-indigo-500 rounded"></div>
            <div class="h-2 bg-slate-500 rounded"></div>
          </div>
        </div>
      </div>

      <div class="shadow-md bg-indigo-50 p-10 h-44 text-center rounded">
        <div class="animate-pulse flex space-x-4">
          <div class="flex-1 space-y-12 py-1">
            <div class="h-3 bg-orange-500 rounded"></div>
            <div class="h-2 bg-slate-500 rounded"></div>
          </div>
        </div>
      </div>

      <div class="shadow-md bg-indigo-50 p-10 h-44 text-center rounded">
        <div class="animate-pulse flex space-x-4">
          <div class="flex-1 space-y-12 py-1">
            <div class="h-3 bg-red-400 rounded"></div>
            <div class="h-2 bg-slate-500 rounded"></div>
          </div>
        </div>
      </div>

      <div class="shadow-md bg-indigo-50 p-10 h-44 text-center rounded">
        <div class="animate-pulse flex space-x-4">
          <div class="flex-1 space-y-12 py-1">
            <div class="h-3 bg-green-500 rounded"></div>
            <div class="h-2 bg-slate-500 rounded"></div>
          </div>
        </div>
      </div>
    </div>

    <select class="form-select block w-full border p-3 rounded mt-10 pointer-events-none">
      <option>{{ currCountry }}</option>
    </select>
  </div>
</template>
