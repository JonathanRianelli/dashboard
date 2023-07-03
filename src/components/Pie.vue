<template>
  <apexchart  class="flex flex-center" type="pie" height="100%"  :options="chartOptions" :series="series"></apexchart>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    return {
      series: [25, 15, 44, 55, 41, 17],
      chartOptions: {
        chart: {
          type: "pie",
        },
        labels: [
          "smartphones",
          "laptops",
          "fragrances",
          "automotive",
          "lighting",
          "home-decoration",
        ],
        theme: {
          monochrome: {
            enabled: true,
          },
        },
        plotOptions: {
          pie: {
            dataLabels: {
              offset: -5,
            },
          },
        },
        title: {
          text: "Main categories",
        },
        dataLabels: {
          formatter(val, opts) {
            const name = opts.w.globals.labels[opts.seriesIndex];
            return [name, val.toFixed(1) + "%"];
          },
        },
        legend: {
          show: false,
        },
      },
    };
  },
});
</script>
