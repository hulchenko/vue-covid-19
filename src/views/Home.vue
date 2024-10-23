//TODO test with no data

<script setup>
import { ref, onMounted } from "vue";
const API_KEY = import.meta.env.VITE_API_KEY;

import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

const loading = ref(true);
const loadingImage = new URL("../assets/loading.gif", import.meta.url).href;

const stats = ref({
  country: "",
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
    console.log(`DATA: `, data);

    if (Array.isArray(data)) {
      return data[0];
    }
    return null;
  } catch (error) {
    console.error("Error fetching data: ", error);
  }
};

const countryChangeHandler = async (country) => {
  console.log(`SELECTED COUNTRY: `, country);
  const data = await fetchCovidData(country);
  stats.value = data;
  loading.value = false;
};

const clearCountryData = async (e) => {
  // loading.value = true;
  // const data = await fetchCovidData();
  // stats.value = "Canada";
  // loading.value = false;
};

// Lifecycle hook on init load

onMounted(async () => {
  const data = await fetchCovidData();
  stats.value = data;
  loading.value = false;
});
</script>

<template>
  <main v-if="!loading">
    <DataTitle :stats="stats" />
    <DataBoxes :stats="stats" />
    <CountrySelect @changeCountry="countryChangeHandler" :loading="loading" />

    <button
      @click="clearCountryData"
      v-if="stats?.Country"
      class="float-right bg-blue-500 text-white rounded p-5 w-3/12 mt-10 focus:outline-none hover:bg-blue-400 border-red-500"
    >
      Reset
    </button>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-red-400 text-2xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="w-14 m-auto" alt="loading" />
  </main>
</template>
