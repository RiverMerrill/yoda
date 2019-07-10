<template>
  <v-layout wrap>
    <h2>Upcoming Yoda: {{ 'George Olson - Drugs' }}</h2>
    <nuxt-link to="/add">
      <v-btn
        color="primary"
        fixed
        top
        right
        outline
        small
        dark
        bottom
      >
        Add a Session
      </v-btn>
    </nuxt-link>
    <v-flex
      xs12
      class="mb-3"
    >
      <h2 class="text-xs-center primary--text">{{currentMonth}}</h2>
      <v-sheet height="500">
        <v-calendar
          ref="calendar"
          v-model="start"
          :type="type"
          color="primary"
        >
          <template v-slot:day="{ date }">
            <template v-for="event in eventsMap[date]">
              <v-menu
                :key="event.title"
                v-model="event.open"
                full-width
                offset-x
              >
                <template v-slot:activator="{ on }">
                  <div
                    v-if="!event.time"
                    v-ripple
                    class="my-event"
                    v-on="on"
                    v-html="event.title"
                  ></div>
                </template>
                <v-card
                  class="event-card"
                  color="grey lighten-4"
                  min-width="350px"
                  flat
                >
                  <v-toolbar
                    color="primary"
                    dark
                  >
                    <v-btn icon>
                      <v-icon>edit</v-icon>
                    </v-btn>
                    <v-toolbar-title v-html="event.title"></v-toolbar-title>
                  </v-toolbar>
                  <v-card-title primary-title>
                    <span v-html="event.details"></span>
                  </v-card-title>
                  <v-card-actions>
                    <v-btn
                      flat
                      color="secondary"
                    >
                      Cancel
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-menu>
            </template>
          </template>
        </v-calendar>
      </v-sheet>
    </v-flex>

    <v-flex xs1>
      <v-btn
        outline
        small
        color="primary"
        @click="$refs.calendar.prev()"
      >
        <v-icon dark>
          keyboard_arrow_left
        </v-icon>
      </v-btn>
    </v-flex>
    <v-spacer></v-spacer>
    <v-flex xs1>
      <v-btn
        outline
        small
        color="primary"
        @click="$refs.calendar.next()"
      >
        <v-icon dark>
          keyboard_arrow_right
        </v-icon>
      </v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'
import * as moment from 'moment';
export default {
  data: () => ({
    type: 'month',
    start: Date.now().date,
    end: Date.now().date,
    events: []
  }),
  computed: {
    currentMonth: function () {
      return moment(this.start).format('MMMM');
    },
    eventsMap() {
      const map = {}
      this.events.forEach(e => (map[e.date] = map[e.date] || []).push(e))
      return map
    }
  }
}
</script>
