<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <h3 class="font-weight-regular my-2">
        @{{ event.time }} on {{ event.date }}
      </h3>
      <h1 class="display-3 font-weight-bold my-7">{{ event.title }}</h1>
      <h4 class="mt-2 font-weight-regular">
        Organized by {{ event.organizer ? event.organizer.name : '' }}
      </h4>
      <h4 class="mb-7 font-weight-regular">Category: {{ event.category }}</h4>
      <h1>Location</h1>
      <h4 class="font-weight-regular mb-7">{{ event.location }}</h4>
      <h1>Event details</h1>
      <h4 class="font-weight-regular mb-7">{{ event.description }}</h4>
      <v-badge color="teal">
        <template v-slot:badge>{{
          event.attendees ? event.attendees.length : 0
        }}</template>
        <h1>Attendees</h1>
      </v-badge>
      <div class="ml-4">
        <h5
          v-for="(attendee, index) in event.attendees"
          :key="index"
          class="font-weight-regular"
        >
          {{ attendee.name }}
        </h5>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import { mapState } from 'vuex'

export default {
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `What you need to know about ${this.event.title}`
        }
      ]
    }
  },
  computed: mapState({
    event: (state) => state.events.event
  }),
  async fetch({ store, error, params }) {
    try {
      await store.dispatch('events/fetchEvent', params.id)
    } catch (e) {
      error({
        statusCode: 503,
        message: `Unable to fetch event #${params.id}`
      })
    }
  }
}
</script>
