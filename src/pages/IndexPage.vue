<template>
  <q-page>
    <h1 >
      Dashboard
    </h1>

    <div class="flex row justify-between wrap" style="gap: 20px;max-width: 95vw; margin: 0 auto;">
      <div class="flex column justify-between" style="gap: 20px">
        <div id="bar" style="border-radius: 10px">
          <bar />
        </div>
        <div id="column" style="border-radius: 10px; background-color: white">
          <column />
        </div>
      </div>

      <div>
        <div id="pie">
          <pie />
        </div>
      </div>
    </div>

    <div>
      <products />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, onMounted } from "vue";
import { useQuasar } from "quasar";
import column from "../components/Column.vue";
import bar from "../components/Bar.vue";
import pie from "../components/Pie.vue";
import products from "../components/Products.vue";

export default defineComponent({
  name: "IndexPage",

  components: {
    column,
    bar,
    pie,
    products,
  },

  setup() {
    const $q = useQuasar();

    onMounted(() => {
      $q.notify({
        message: "Bem vindo",
        color: "purple",
      });
    });

    return {};
  },
});
</script>
