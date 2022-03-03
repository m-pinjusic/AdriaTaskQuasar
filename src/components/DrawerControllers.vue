<template>
  <q-item clickable tag="a" :to="'/controller/' + id">
    <q-item-section>
      <q-item-label>{{ name }}</q-item-label>
      <q-item-label caption> Adresa: {{ address }} </q-item-label>
    </q-item-section>
  </q-item>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "DrawerControllers",
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
});
</script>
