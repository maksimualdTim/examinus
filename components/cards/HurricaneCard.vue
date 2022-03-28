<template>
  <div class="HurricaneCard">
    <v-img src="hurricane_img.jpg" max-height="300" max-width="300"></v-img>
    <v-card-title>{{event.type}}</v-card-title>
    <v-card-subtitle>{{event.date}}</v-card-subtitle>
    <v-card-text>victims: {{event.victims}}</v-card-text>
    <v-card-text>wind_speed: {{event.wind_speed}}</v-card-text>
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
  name: "HurricaneCard"
}
</script>

<style scoped>

</style>
