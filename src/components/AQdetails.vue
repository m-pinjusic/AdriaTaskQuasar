<template>
  <div class="col-shrink">
    <q-chip
      color="white"
      text-color="black"
      size="lg"
      dense
      style="width: 220px"
    >
      <div class="absolute-center">
        {{ title }}:&nbsp;{{ value }}&nbsp;{{ unit }}
      </div>

      <q-tooltip
        transition-show="scale"
        transition-hide="scale"
        class="bg-white text-black shadow-4"
        flat
        bordered
      >
        <q-item>
          <q-item-section>
            <q-item-label>
              <h6 text-h6 class="q-ma-xs">{{ title }}</h6></q-item-label
            >

            <q-item-label caption>
              Prosjek: {{ averageValue.toFixed(1) }} &emsp; <br />Zadnje
              ažurirano:
              {{ this.formatDate }}
            </q-item-label>
          </q-item-section>
        </q-item>
      </q-tooltip>
    </q-chip>
  </div>
</template>

<script>
import { date } from "quasar";
import { defineComponent } from "vue";
export default defineComponent({
  name: "AQdetails",

  data() {
    return {
      formatDate: "",
    };
  },

  props: {
    name: {
      type: String,
      default: "",
    },

    value: {
      type: Number,
      default: 0,
    },
    title: {
      type: String,
      default: "",
    },

    averageValue: {
      type: Number,
      default: 0,
    },

    lastDate: {
      type: String,
      default: "",
    },
    unit: {
      type: String,
      default: "",
    },
  },
  mounted() {
    this.formatDate = date.formatDate(this.lastDate, "DD.MM.YYYY.");
  },
});
</script>
