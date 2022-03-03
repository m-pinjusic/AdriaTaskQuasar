<template>
  <q-card class="my-card col-shrink q-ma-sm">
    <q-card-section class="bg-primary text-white">
      <div class="text-h6">Zona: {{ zone }}</div>
      <div class="text-subtitle2">Naziv: {{ name }}</div>
      <div class="text-subtitle2">Adresa: {{ address }}</div>
    </q-card-section>

    <q-separator />

    <q-card-actions align="right">
      <QRgenerator :controllerName="name" />
      <q-btn size="md" flat :to="'/controller/' + id">Detalji</q-btn>
    </q-card-actions>
  </q-card>
</template>

<script>
import QRgenerator from "components/QRgenerator.vue";

export default {
  components: {
    QRgenerator,
  },
  props: {
    name: {
      type: String,
      required: true,
    },

    zone: {
      type: String,
      default: "",
    },
    address: {
      type: Number,
      default: 0,
    },
    id: {
      type: Number,
      default: 0,
    },
  },
  setup() {
    return {};
  },
  data() {
    return {};
  },
};
</script>

<style lang="sass" scoped>
.my-card
  min-width: 20%

  height: 160px
</style>
