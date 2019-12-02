<template>
  <nuxt-link :to="`/event/${event.id}`">
    <v-card
      :raised="raised"
      @mouseenter="raised = true"
      @mouseleave="raised = false"
      class="mt-3"
      style="width: 400px;"
    >
      <v-card-text>
        <h3 class="teal--text font-weight-regular mb-1">
          @{{ event.time }} on {{ parsedDate }}
        </h3>
        <h2 class="grey--text text--darken-4">{{ event.title }}</h2>
        <h3 class="teal--text font-weight-regular mt-1">
          {{ event.attendees.length }} attending
        </h3>
      </v-card-text>
    </v-card>
  </nuxt-link>
</template>

<script>
export default {
  name: 'EventCard',
  props: {
    event: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
      raised: false
    }
  },
  computed: {
    parsedDate() {
      const eventDate = new Date(this.event.date)
      return eventDate.toDateString()
    }
  }
}
</script>

<style>
a {
  text-decoration: none;
}
</style>
