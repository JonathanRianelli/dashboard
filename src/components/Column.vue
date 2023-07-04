<template>
  <apexchart
    class="flex flex-center"
    type="bar"
    height="100%"
    :options="options"
    :series="series"
  ></apexchart>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
import { api } from "boot/axios";

export default defineComponent({
  name: "App",
  setup() {
    let series = ref([
      {
        name: "Sales",
        data: [],
      },
    ]);

    let options = ref({
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
          return val + "$";
        },
        offsetY: -20,
        style: {
          fontSize: "12px",
          colors: ["#304758"],
        },
      },

      xaxis: {
        categories: [],
        position: "top",
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
        labels: {
          style: {
            fontSize: "10px",
            align: "center",
          },
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
            return val + "$";
          },
        },
      },
      title: {
        text: "Average Prices",
        floating: false,
        offsetY: 1,
        align: "left",
        style: {
          color: "#444",
        },
      },
      noData: {
        text: "Loading...",
      },
    });

    const productsPrice = () => {
      api
        .get("https://dummyjson.com/products/")
        .then((res) => {
          const products = res.data.products;

          const price = products.slice(0, 6).map((item) => item.price);
          const name = products.slice(0, 6).map((item) => item.title);

          series.value = [
            {
              data: price,
            },
          ];

          options.value = {
            xaxis: {
              categories: name,
            },
          };
        })
        .catch((err) => {
          console.log(err);
        });
    };

    onMounted(() => {
      productsPrice();
    });

    return {
      series,
      options,
    };
  },
});
</script>
