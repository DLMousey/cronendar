<template>
  <div class="container">
    <CronInput @cronInput="onCronInput"></CronInput>
    <h2>Cron Calendar</h2>
    <div class="calendar-container">
      <!-- eslint-disable-next-line -->
      <CalendarColumn v-for="(n, i) in 7" :day=getDay(i) :entries="this.entries[i]"></CalendarColumn>
    </div>
  </div>
</template>

<script>
import CalendarColumn from "@/components/CalendarColumn";
import CronInput from "@/components/CronInput";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Calendar",
  components: {CronInput, CalendarColumn},
  data() {
    return {
      entries: {
        1: [],
        2: [],
        3: [],
        4: [],
        5: [],
        6: [],
        7: []
      }
    }
  },
  methods: {
    getDay(number) {
      switch(number) {
        case 1:
          return "Monday"
        case 2:
          return "Tuesday"
        case 3:
          return "Wednesday"
        case 4:
          return "Thursday"
        case 5:
          return "Friday"
        case 6:
          return "Saturday"
        case 7:
        case 0:
          return "Sunday"
      }
    },
    onCronInput(input) {
      this.entries = {
        0: [],
        1: [],
        2: [],
        3: [],
        4: [],
        5: [],
        6: [],
      }

      input.forEach(entry => {
        this.entries[entry.day.number].push(entry);
      });
    }
  }
}
</script>

<style scoped>
h2 {
  display: block;
  width: 100%;
}
.calendar-container {
  display: flex;
  justify-content: center;
}
</style>
