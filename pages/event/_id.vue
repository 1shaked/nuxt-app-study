<template>
  <div>
    <div class="event-header">
      <span class="eyebrow">
        @{{ event.time }} on {{ event.date }}
      </span>
      <h1 class="title">
        {{ event.title }}
      </h1>
      <h5>Organized by {{ event.organizer ? event.organizer.name : '' }}</h5>
      <h5>Category: {{ event.category }}</h5>
    </div>

    <span name="map">
      <h2>Location</h2>
    </span>

    <address>{{ event.location }}</address>

    <h2>Event details</h2>
    <p>{{ event.description }}</p>

    <h2>
      Attendees
      <span class="badge -fill-gradient">
        {{ event.attendees ? event.attendees.length : 0 }}
      </span>
    </h2>
    <ul class="list-group">
      <li v-for="(attendee, index) in event.attendees" :key="index" class="list-item">
        <b>{{ attendee.name }}</b>
      </li>
    </ul>
  </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  head() {
    return {
      title: 'Event id is ' + this.event.id ,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'You can create a new event in your neighborhood'
        }
      ]
    }
  },
  async fetch({ error, store, params }) {
    try {
      store.dispatch('events/fetchEvent' , params.id)
    } catch (error) {
      error({
        statusCode: 503,
        message: 'Unable to get the this event data pls try choose another one'
      })
    }
  },
  computed: mapState({
    event: state => state.events.event
  })
}
</script>
<style scoped>
.prompt-box {
  position: relative;
  overflow: hidden;
  padding: 1em;
  margin-bottom: 24px;
  transform: scaleY(1);
}
.prompt-box > .title {
  margin: 0 0 0.5em;
}
.prompt-box > .title > .meta {
  margin-left: 10px;
}
.prompt-box > .actions {
  display: flex;
  align-items: center;
}
.prompt-box > button {
  margin-right: 0.5em;
}
.prompt-box > button:last-of-type {
  margin-right: 0;
}
.location {
  margin-bottom: 0;
}
.location > .icon {
  margin-left: 10px;
}
.event-header > .title {
  margin: 0;
}
.list-group {
  margin: 0;
  padding: 0;
  list-style: none;
}
.list-group > .list-item {
  padding: 1em 0;
  border-bottom: solid 1px #e5e5e5;
}
</style>

