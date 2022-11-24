<template>
  <div class="container">
    <sup class="hour-label">{{ getHourLabel($props.hour) }}</sup>
    <!-- eslint-disable-next-line -->
    <span class="entry-badge" v-for="entry in $props.entries">{{ entry.expression }}</span>
  </div>
</template>

<script>
export default {
  name: "CalendarCell",
  props: ['hour', 'entries'],
  methods: {
    getHourLabel(hour) {
      if (hour === 24) {
        return "00:00";
      }

      if (hour < 10) {
        return `0${hour}:00`;
      }

      return `${hour}:00`;
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  /*border: 1px solid #EBEBEB;*/
  width: 100%;
  padding: 8px;
  border-bottom: 1px dashed #ebebeb;
  min-height: 45px;
  position: relative;
}

.hour-label {
  color: #999;
  /*display: block;*/
  /*width: 100%;*/
  position: absolute;
  top: 0;
  left: 5px;
}

.entry-badge {
  background: blue;
  color: white;
  border: none;
  padding: 12px;
  display: block;
  border-radius: 6px;
  margin-top: 6px;
}
</style>
