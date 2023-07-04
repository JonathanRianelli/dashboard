<template>
  <apexchart
    class="flex flex-center"
    type="pie"
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
    let series = ref([]);

    let options = ref({
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
        text: "Stock",
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
    });

    const productsStock = () => {
      api
        .get("https://dummyjson.com/products/")
        .then((res) => {
          const products = res.data.products;

          const stock = products.slice(0, 6).map((item) => item.stock);
          const name = products.slice(0, 6).map((item) => item.title);

          series.value = stock

          options.value = {
            labels: name,
          };
        })
        .catch((err) => {
          console.log(err);
        });
    };

    onMounted(() => {
      productsStock();
    });

    return {
      series,
      options,
    };
  },
});
</script>
