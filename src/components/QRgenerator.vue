<template>
  <q-btn
    :class="classProp"
    :color="colorProp"
    :size="sizeProp"
    :flat="flatProp"
    @click="alert = true"
  >
    QR kod
  </q-btn>

  <q-dialog v-model="alert">
    <q-card>
      <q-card-section>
        <div class="text-h6">QR code for {{ controllerName }}</div>
      </q-card-section>
      <q-card-section class="q-pt-none">
        <q-img :src="urlQR" alt="QR code" title="" center />
      </q-card-section>

      <q-card-actions align="right">
        <q-btn flat label="OK" color="primary" v-close-popup />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";

export default defineComponent({
  setup() {
    return {
      alert: ref(false),
      address: ref(""),
    };
  },
  data() {
    return {
      urlQR:
        "https://api.qrserver.com/v1/create-qr-code/?data=" +
        this.controllerName +
        "&amp;size=100x100",
    };
  },
  name: "QRgenerator",

  props: {
    controllerName: {
      type: String,
      default: "",
    },
    classProp: {
      type: String,
      default: "",
    },
    colorProp: {
      type: String,
      default: "",
    },
    flatProp: {
      type: Boolean,
      default: true,
    },
    sizeProp: {
      type: String,
      default: "",
    },
  },
});
</script>
