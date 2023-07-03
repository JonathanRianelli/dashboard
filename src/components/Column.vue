<template>
  <apexchart
    class="flex flex-center"
    type="bar"
    height="100%"
    :options="chartOptions"
    :series="series"
  ></apexchart>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    return {
      series: [
        {
          name: "Sales",
          data: [2.3, 3.1, 4.0, 10.1, 4.0, 3.6],
        },
      ],

      chartOptions: {
        chart: {
          height: 350,
          type: "bar",
        },
        plotOptions: {
          bar: {
            borderRadius: 5,
            dataLabels: {
              position: "top", // top, center, bottom
            },
          },
        },
        dataLabels: {
          enabled: true,
          formatter: function (val) {
            return val + "k";
          },
          offsetY: -20,
          style: {
            fontSize: "12px",
            colors: ["#304758"],
          },
        },

        xaxis: {
          categories: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
          position: "bottom",
          axisBorder: {
            show: true,
          },
          axisTicks: {
            show: false,
          },
          crosshairs: {
            fill: {
              type: "gradient",
              gradient: {
                colorFrom: "#D8E3F0",
                colorTo: "#BED1E6",
                stops: [0, 100],
                opacityFrom: 0.4,
                opacityTo: 0.5,
              },
            },
          },
          tooltip: {
            enabled: true,
          },
        },
        yaxis: {
          axisBorder: {
            show: false,
          },
          axisTicks: {
            show: false,
          },
          labels: {
            show: false,
            formatter: function (val) {
              return val + "k";
            },
          },
        },
        title: {
          text: "Semester sales",
          floating: false,
          offsetY: 1,
          align: "center",
          style: {
            color: "#444",
          },
        },
      },
    };
  },
});
</script>
