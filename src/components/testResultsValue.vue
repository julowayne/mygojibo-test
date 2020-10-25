<template>
  <div class="result">
    <div class="icon">
      <img v-if="testResultValue" :src="nameImages" alt="name image" />
    </div>
    <div class="info">
      <div class="name">{{ testResultValue.name }}</div>
      <div class="date">{{ formatDate }}</div>
    </div>
    <div class="score">{{ testResultValue.score }}%</div>
    <div class="bar">
      <div class="progress">
        <div
          class="progress-bar"
          role="progressbar"
          :style="{ width: `${testResultValue.score}%` }"
          :aria-valuenow="testResultValue"
          aria-valuemin="0"
          aria-valuemax="100"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
import "bootstrap";
import "jquery";
import "popper.js";
import dayjs from "dayjs";
var customParseFormat = require("dayjs/plugin/customParseFormat");
dayjs.extend(customParseFormat);
var relativeTime = require("dayjs/plugin/relativeTime");
dayjs.extend(relativeTime);
export default {
  name: "testResultsValue",
  props: {
    testResultValue: Object
  },
  computed: {
    nameImages() {
      const image = this.testResultValue.name.toLowerCase();
      return require(`../assets/${image}.png`);
    },
    formatDate() {
      var date = dayjs(this.testResultValue.date, "D/MM/YYYY");
      return date.fromNow();
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~bootstrap/scss/bootstrap";
.result {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1em;
  text-align: left;
  .icon {
    margin-right: 1rem;
  }
  .info {
    flex-basis: 40%;
    .name {
      color: $black;
    }

    .date {
      color: $text-muted;
    }
  }

  .score {
    color: $text-muted;
    text-align: right;
    margin-right: 0.5rem;
    font-size: large;
    flex-basis: 25%;
  }
  .bar {
    flex-basis: 25%;
    .progress {
      height: 20px;
      background-color: $gray-300;
      box-shadow: none;
      .progress-bar {
        background-color: $teal;
      }
    }
  }
}
@media (max-width: 504px) {
  .result {
    .bar {
      .progress {
        height: 15px;
      }
    }
  }
}
</style>
