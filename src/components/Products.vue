<template>
  <q-page>
    <q-table
      id="table"
      title="Products"
      :rows="rows"
      :columns="columns"
    >
      <template v-slot:body-cell-img="props">
        <q-td :props="props" style="padding: 0; height: 70px">
          <img
            :src="props.row.thumbnail"
            style="max-height: 70px; margin-left: 10px"
          />
        </q-td>
      </template>
    </q-table>
  </q-page>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
import { useQuasar } from "quasar";
import { api } from "boot/axios";

export default defineComponent({
  name: "App",

  setup() {
    const $q = useQuasar();

    const columns = [
      {
        label: "Thumbnail",
        field: "img",
        name: "img",
        align: "left",
      },
      {
        label: "Name",
        field: "title",
        name: "title",
        align: "left",
      },
      {
        label: "Brand",
        field: "brand",
        name: "brand",
        align: "left",
      },
      {
        label: "Category",
        field: "category",
        name: "Category",
        align: "center",
      },
    ];

    const rows = ref();

    const getPosts = () => {
      api
        .get("https://dummyjson.com/products")
        .then((res) => {
          rows.value = res.data.products;
        })
        .catch((err) => {
          $q.notify({
            color: "negative",
            position: "top",
            message: "Loading failed",
            icon: "report_problem",
          });
        });
    };

    onMounted(() => {
      getPosts();
    });

    return {
      rows,
      columns,
    };
  },
});
</script>
