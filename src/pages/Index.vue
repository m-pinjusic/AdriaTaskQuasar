<template>
  <q-page class="flex">
    <div class="q-ma-md row content-start justify-start items-center">
      <ControllerShortList
        v-for="data in basicControllersData"
        :key="data.id"
        v-bind="data"
      >
      </ControllerShortList>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import ControllerShortList from "components/ControllerShortList.vue";

export default defineComponent({
  name: "PageIndex",
  components: {
    ControllerShortList,
  },
  data() {
    return {
      basicControllersData: [],
    };
  },
  async mounted() {
    this.basicControllersData = this.$q.sessionStorage.getItem(
      "sessionControllerData"
    );
  },
});
</script>
