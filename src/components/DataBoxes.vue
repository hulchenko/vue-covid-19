<script setup>
const { stats = {} } = defineProps(["stats"]);
const { confirmed = 0, critical = 0, deaths = 0, recovered = 0 } = stats;

const numberWithCommas = (i) => {
  return i.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
};
</script>

<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow-md bg-indigo-50 p-10 text-center rounded h-44">
      <h3 class="text-3xl text-indigo-500 font-bold mb-4">Cases</h3>
      <div class="text-2xl mb-4">
        {{ numberWithCommas(confirmed) }}
      </div>
    </div>

    <div class="shadow-md bg-indigo-50 p-10 text-center rounded h-44">
      <h3 class="text-3xl text-orange-500 font-bold mb-4">Critical</h3>
      <div class="text-2xl mb-4">
        {{ numberWithCommas(critical) }}
      </div>
    </div>

    <div class="shadow-md bg-indigo-50 p-10 text-center rounded h-44">
      <h3 class="text-3xl text-red-400 font-bold mb-4">Deaths</h3>
      <div class="text-2xl mb-4">
        {{ numberWithCommas(deaths) }}
      </div>
    </div>

    <div class="shadow-md bg-indigo-50 p-10 text-center rounded h-44">
      <h3 class="text-3xl text-green-500 font-bold mb-4">Recovered</h3>
      <div class="text-2xl mb-4">
        {{ numberWithCommas(recovered) }}
      </div>
    </div>
  </div>
</template>
