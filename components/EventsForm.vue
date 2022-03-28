<template>
  <form>
    <v-row>
      <v-col>
        <v-select :items="typeItems" @change="defineEvent" v-model="new_event.type"></v-select>
        <v-text-field v-if="typeIsSelected" :label="label" v-model="new_event.power"></v-text-field>
      </v-col>
      <v-col>
        <v-date-picker v-model="new_event.date"></v-date-picker>
      </v-col>
      <v-col>
        <v-text-field label="Victims" v-model="new_event.victims"></v-text-field>
      </v-col>
      <v-col>
        <v-btn
          class="mr-4"
          @click="sendEvent"
        >
          submit
        </v-btn>
      </v-col>
    </v-row>
  </form>
</template>
<script>

export default  {
  props:{
    new_event:{
      type: Object,
      required: true,
    },
    typeItems:{
      type: Array,
      required: true,
    }
  },
  data(){
    return {
      typeIsSelected: false,
    }
  },
  methods:{
    sendEvent(action){
      this.$emit('sendEvent')
    },
    defineEvent(action){
      this.typeIsSelected = true

      switch(this.new_event.type){
        case this.typeItems[0]:
          this.label = 'Сила кислоты'
          break;
        case this.typeItems[1]:
          this.label = 'Скорость ветра'
          break;
        case this.typeItems[2]:
          this.label = 'Амплитуда землетрясения'
          break;
      }
      this.$emit('powerLabel', this.label)
    },
  }
}
</script>
