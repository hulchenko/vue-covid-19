<script setup>
import moment from "moment";

const { stats } = defineProps(["stats"]);
const { country, lastUpdate } = stats;

const timestamp = () => {
  if (lastUpdate) {
    return moment(lastUpdate).format("MMMM Do YYYY, h:mm A") + " MDT";
  }
  return "Unknown";
};
</script>

<template>
  <div class="text-center border-red-400">
    <h2 class="text-3xl font-bold">{{ country }}</h2>
    <div class="text-2xl mt-4 mb-10">Last updated: {{ timestamp() }}</div>
  </div>
</template>
