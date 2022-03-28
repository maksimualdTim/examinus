<template>
  <div class="AcidrainCard">
    <v-img src="rain_img.jpg" max-height="300" max-width="300"></v-img>
    <v-card-title>{{event.type}}</v-card-title>
    <v-card-subtitle>{{event.date}}</v-card-subtitle>
    <v-card-text>victims: {{event.victims}}</v-card-text>
    <v-card-text>acid_power: {{event.acid_power}}</v-card-text>
  </div>
</template>

<script>
export default {
  props:{
    event:{
      type: Object,
      required: true
    }
  },
  name: "AcidrainCard"
}
</script>

<style scoped>

</style>
