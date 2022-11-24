<template>
  <div class="column">
    <div class="column-heading" :title="getTitle()">
      <b class="day-label">{{ $props.day }} <sup>({{ ($props.entries) !== undefined ? $props.entries.length : 0 }})</sup></b>
    </div>
    <div class="column-body">
        <!-- eslint-disable-next-line -->
        <CalendarCell v-for="(n, i) in 24" :hour="i" :entries="getEntries(i)"></CalendarCell>
    </div>
  </div>
</template>

<script>
import CalendarCell from "@/components/CalendarCell";
export default {
  name: "CalendarColumn",
  components: {CalendarCell},
  props: ['day', 'entries'],
  methods: {
    getEntries(hour) {
      if (undefined === this.$props.entries) {
        return [];
      }

      return this.$props.entries.filter(entry => {
        return entry.hour === hour
      });
    },
    getTitle() {
      if (undefined === this.$props.entries) {
        return "No entries";
      }

      switch (this.$props.entries.length) {
        case 0:
          return `There are no jobs scheduled to run on ${this.$props.day}`;
        case 1:
          return `There is 1 job scheduled to run on ${this.$props.day}`;
        default:
          return `There are ${this.$props.entries.length} jobs scheduled to run on ${this.$props.day}`
      }
    }
  }
}
</script>

<style scoped>
.column {
  border: 1px solid #EBEBEB;
  border-right: none;
}

.column:last-child {
  border-right: 1px solid #EBEBEB;
}

.column-heading {
  padding: 12px;
  border-bottom: 1px solid #EBEBEB;
}

.column-body {
  display: flex;
  flex-direction: column;
  width: 100%;
  flex-grow: 1;
  flex-shrink: 0;
}
</style>
