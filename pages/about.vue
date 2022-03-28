<template>
  <v-container>
    <v-row>
      <v-col>{{about.text}}</v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'InspirePage',
  data(){
    return{
      about: {}
    }
  },
  mounted(){
    this.fetchAboutInfo()
  },
  methods:{
    async fetchAboutInfo(){
      this.about = await this.$axios.$get('https://demo-api.vsdev.space/api/elonus/about_page')
    }
  }
}
</script>
