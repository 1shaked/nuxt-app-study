<template>
  <div class="container">
    <EventCard
    v-for="(event, index) in events"
    :key="index"
    :event="event"
    :data-index="index"></EventCard>
  </div>
</template>

<script>
// import EventService from '@/services/EventService.js'
import Logo from '~/components/Logo.vue'
import EventCard from '~/components/EventCard.vue'
import { mapState } from 'vuex'
export default {
  components: {
    Logo,
    EventCard
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (error) {
      error({
        statusCode: 503,
        message: 'Unable to get the data from the api pls refresh and try agine'
      })
    }
  },
  computed: mapState({
    events: state => state.events.events
  })
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
