<script setup>
import moment from "moment";

const { stats = {} } = defineProps(["stats"]);
const { country = "Unknown", lastUpdate = null } = stats;

const timestamp = () => {
  const displayData = moment(lastUpdate).format("MMMM Do YYYY, h:mm A") + " MDT";
  return lastUpdate ? displayData : "Unknown";
};
</script>

<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ country }}</h2>
    <div class="text-2xl mt-4 mb-10">Last updated: {{ timestamp() }}</div>
  </div>
</template>
