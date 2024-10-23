<script setup>
const props = defineProps({
  stats: Object,
});
console.log(`props: `, props);
const numberWithCommas = (i) => {
  // return i.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
  return i;
};
</script>

<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow-md bg-blue-50 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-500 font-bold mb-4">Cases</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold text-blue-900">New:</span>
        {{ numberWithCommas(stats?.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold text-blue-900">Total:</span>
        {{ numberWithCommas(stats?.TotalConfirmed) }}
      </div>
    </div>

    <div class="shadow-md bg-blue-50 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-500 font-bold mb-4">Deaths</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold text-blue-900">New:</span>
        {{ numberWithCommas(stats?.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold text-blue-900">Total:</span>
        {{ numberWithCommas(stats?.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>
