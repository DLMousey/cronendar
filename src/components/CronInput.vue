<template>
  <div class="container">
    <textarea v-model="cron" class="cron-input" name="crontab" placeholder="Paste a crontab here" />
    <button class="cron-button" @click="generate()" type="button">Generate calendar</button>
  </div>
</template>

<script>
export default {
  name: "CronInput",
  data() {
    return {
      cron: ""
    }
  },
  methods: {
    generate() {
      const raw = this.cron;
      const lines = raw.split('\n').filter(val => val !== "");
      const pairs = [];

      const parser = require('cron-parser');
      lines.forEach(line => {
        const parsed = parser.parseString(line);
        parsed.expressions[0].fields.dayOfWeek.forEach(dow => {
          if (dow === 7) {
            return;
          }

          pairs.push({
            expression: line,
            normalisedExpression: line.replaceAll(' ', ''),
            day: {
              name: this.getDay(dow),
              number: dow
            },
            hour: parsed.expressions[0].fields.hour[0]
          })
        })
      })

      this.$emit('cronInput', pairs);
    },
    getDay(number) {
      switch(parseInt(number, 10)) {
        case 0:
          return "Sunday"
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
      }
    },
  }
}
</script>

<style scoped>
  .container {
    display: flex;
    width: 50%;
    height: auto;
    margin: 0 auto;
    justify-content: center;
  }

  .cron-input {
    display: block;
    border: 1px solid #999;
    border-radius: 4px 0 0 4px;
    padding: 12px;
  }

  .cron-button {
    display: block;
    background: #666;
    border: none;
    border-radius: 0 4px 4px 0;
    padding: 12px;
    font-size: 12px;
    text-transform: uppercase;
    font-weight: bold;
    color: #FFF;
    cursor: pointer;
  }
</style>
