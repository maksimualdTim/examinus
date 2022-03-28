<template>
  <v-card
    class="mx-auto"
    height="400"
    width="256"
  >
    <v-img src="left_widget_img.jpg"></v-img>
    {{left_widget.events}}
  </v-card>

</template>
<script>
export default {
  data () {
    return {
      left_widget: {}
    }
  },
  methods:{
    async fetchLeftWidget(){
      this.left_widget = await this.$axios.$get('https://demo-api.vsdev.space/api/elonus/left_widget')
    },

  },
  mounted(){
    this.fetchLeftWidget()
  }
}
</script>
