<template>
  <v-container>
    <v-row>
      <v-col>
        <v-expansion-panels>
          <v-expansion-panel>
            <v-expansion-panel-header>
              <v-btn>Add Event</v-btn>
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              <events-form
                @powerLabel="setPowerLabel"
                v-bind:new_event="new_event"
                @sendEvent="sendEvent"
                v-bind:typeItems="typeItems"></events-form>
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
      </v-col>
    </v-row>
    <v-row>
      <v-col v-for="event in events" :key="event.id" cols="12" md="2">
        <v-card v-if="event.type === 'acid_rain'">
          <cards-acidrain-card v-bind:event="event"></cards-acidrain-card>
        </v-card>
        <v-card v-else-if="event.type === 'earthquake'">
          <cards-earthquake-card v-bind:event="event"></cards-earthquake-card>
        </v-card>
        <v-card v-if="event.type === 'hurricane'">
          <cards-hurricane-card v-bind:event="event"></cards-hurricane-card>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: 'EventsPage',
  components: {},

  data(){
    return {
      events:{},
      new_event: {},
      eventsForm: [],
      typeItems: [],
      typePower: '',
      label:'',
    }
  },
  methods:{
    async fetchEvents(){
      this.events = await this.$axios.$get('https://demo-api.vsdev.space/api/elonus/events')
    },
    async fetchEventsForm(){
      this.eventsForm = await this.$axios.$get('https://demo-api.vsdev.space/api/elonus/events/form')

      this.typeItems = this.eventsForm.fields.type.values
    },
    setPowerLabel(label){
      this.label =  label
    },
    sendEvent(action){
      let fd = new FormData()
      fd.append('date', this.new_event.date)
      fd.append('type', this.new_event.type)
      fd.append('victims', this.new_event.victims)
      switch(this.label){
        case 'Сила кислоты':
          fd.append('acid_power', this.new_event.power)
          break;
        case 'Скорость ветра':
          fd.append('wind_speed', this.new_event.power)
          break;
        case 'Амплитуда землетрясения':
          fd.append('earthquake_power', this.new_event.power)
          break;
      }
      fetch(
        "https://demo-api.vsdev.space/api/elonus/events",
        {
          method: "POST",
          headers: {
            "Accept": 'application/json',
          },
          body: fd
        },
      )
      this.fetchEvents()
    },
  },
  mounted(){
    this.fetchEvents()
    this.fetchEventsForm()
  }
}
</script>
