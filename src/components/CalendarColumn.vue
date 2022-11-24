<template>
  <div class="column">
    <b>{{ $props.day }}</b>
    <div class="cells">
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
    }
  }
}
</script>

<style scoped>
.column {
  display: flex;
  flex-wrap: wrap;
  flex-grow: 1;
  flex-basis: 21%;
  border: 1px solid #EBEBEB;
  padding: 6px;
  border-radius: 4px;
}

.cells {
  display: flex;
  flex-direction: column;
  width: 100%;
  flex-grow: 1;
  flex-shrink: 0;
}
</style>
