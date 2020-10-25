<template>
  <tr>
    <td>
      <img v-if="testResultValue" :src="nameImages" alt="name image" />
      {{ testResultValue.name }}
    </td>
    <td>{{ formatDate }}</td>
    <td>
      <span>{{ testResultValue.score }}%</span>
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
    </td>
  </tr>
</template>
<script>
import "bootstrap";
import "jquery";
import "popper.js";
import dayjs from "dayjs";
var customParseFormat = require("dayjs/plugin/customParseFormat");
dayjs.extend(customParseFormat);
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
      console.log(this.testResultValue.date);
      return dayjs(this.testResultValue.date, "DD.MM").format("MM.DD");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "~bootstrap/scss/bootstrap";

tr,
td {
  text-align: left;
  color: $gray-600;
  #score {
    color: $black;
  }
  .progress {
    height: 25px;
  }
  td:first-child {
    color: $black;
  }
  td:nth-child(2n) {
    vertical-align: middle;
  }
  td:last-child {
    width: 150px;
    vertical-align: middle;
  }
  img {
    margin-right: 20px;
  }
}
</style>
