<template>
  <apexchart
    type="bar"
    height="100%"
    width="100%"
    :options="options"
    :series="series"
  ></apexchart>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
import { api } from 'boot/axios'

export default defineComponent({
  name: "App",

  setup() {

    let series = ref([
      {
        name: "Rating",
        data: [],
      },
    ]);

    let options = ref({
      chart: {
        type: "bar",
        height: 350,
      },
      plotOptions: {
        bar: {
          borderRadius: 4,
          horizontal: true,
        },
      },
      dataLabels: {
        enabled: false,
      },
      title: {
        text: "Products Rating",
      },
      xaxis: {
        categories: ["", "", "", "", "", ""],
      },
      noData: {
        text: "Loading...",
      },
    });

    const productsRating = () => {
      api.get('https://dummyjson.com/products/')
        .then((res) => {
          const products = res.data.products;

          const sales = products.slice(0, 6).map(item => item.rating);
          const name = products.slice(0, 6).map(item => item.title);

          series.value = [{
            data: sales
          }];

          options.value = {
            xaxis: {
              categories: name,
            },
          }

        })
        .catch((err) => {
          console.log(err)
        })
    }

    onMounted(() => {
      productsRating()
    })

    return {
      series,
      options,
    };
  },
});
</script>
