<template>

  <apexchart
    type="bar"
    height="100%"
    width="100%"
    :options="chartOptions"
    :series="series"
  ></apexchart>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    return {
      series: [
        {
          name: "Sales",
          data: [1380, 1200, 1100, 690, 580, 540, 470, 448, 430, 400],
        },
      ],
      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
        },
        plotOptions: {
          bar: {
            borderRadius: 2,
            horizontal: true,
          },
        },
        dataLabels: {
          enabled: false,
        },
        xaxis: {
          categories: [
            "Canada",
            "United Kingdom",
            "France",
            "Japan",
            "United States",
            "China",
            "Germany",
          ],
        },
        title: {
          text: "Regional performance",
          floating: false,
          offsetY: 1,
          align: "lef",
          style: {
            color: "#444",
          },
        },
      },
    };
  },
});
</script>
