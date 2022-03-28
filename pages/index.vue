<template>
  <v-container>
    <v-row>
      <v-col>
        {{home.text}}
      </v-col>
      <v-col>
        <v-img
          :src="home.image"
          max-height="700"
          max-width="700"></v-img>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'IndexPage',
  data(){
    return {
      home: {}
    }
  },
  mounted(){
    this.fetchHomePage()
  },
  methods:{
    async fetchHomePage(){
      this.home = await this.$axios.$get('https://demo-api.vsdev.space/api/elonus/home_page')
    }
  }
}
</script>
