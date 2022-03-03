<template>
  <div class="q-pa-md row items-start q-gutter-md">
    <q-card class="my-card">
      <q-card-section class="bg-primary text-white">
        <div class="text-h6">Room 101</div>
        <div class="text-subtitle2">Zone: 101</div>
        <div class="text-subtitle2">Address: 101</div>
      </q-card-section>

      <q-separator />

      <q-card-actions align="right">
        <q-btn flat>QR kod</q-btn>
        <q-btn flat>Detalji</q-btn>
      </q-card-actions>
    </q-card>
  </div>
</template>

<script>
export default {
  setup () {
    return {
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
    }
  }
}
</script>

<style lang="sass" scoped>
.my-card
  width: 300px
  min-width: 50%
</style>