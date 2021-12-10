<template>
  <div>
    <h1>{{ this.event.title }}</h1>
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'

export default {
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)
      return {
        event: data,
      }
    } catch (e) {
      error({
        statusCode: 503,
        message:
          'Unable to fetch event #' +
          params.id +
          'at this time. Please try again.',
      })
    }
  },
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'descriptiom',
          name: 'description',
          content: 'What you need to know about ' + this.event.title,
        },
      ],
    }
  },
}
</script>
