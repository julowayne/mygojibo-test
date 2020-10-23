<template>
  <tr>
    <td>
      <img v-if="testResultValue" :src="nameImages" alt="name image" />
      {{ testResultValue.name }}
    </td>
    <td>{{ testResultValue.date }}</td>
    <td id="score">
      <div class="progress" style="height: 25px;">
        <div
          class="progress-bar"
          role="progressbar"
          :style="{ width: `${testResultValue.score}%` }"
          :aria-valuenow="testResultValue"
          aria-valuemin="0"
          aria-valuemax="100"
        >
          {{ testResultValue.score }}%
        </div>
      </div>
    </td>
  </tr>
</template>

<script>
import "bootstrap";
import "jquery";
import "popper.js";
export default {
  name: "testResultsValue",
  props: {
    testResultValue: Object
  },
  computed: {
    nameImages() {
      const image = this.testResultValue.name.toLowerCase();
      return require(`../assets/${image}.png`);
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
  padding: 1em;
  color: $gray-600;
  td:last-child {
    text-align: left;
  }
}
#score {
  padding: 1.5rem 2rem;
  background-color: #e9ecef;
  color: $teal;
  &.very-low,
  &.low,
  &.average,
  &.high {
    color: $gray-600;
  }
  &.very-low {
    background-color: #dc3a12f3;
  }
  &.low {
    background-color: #ff9900;
  }
  &.average {
    background-color: #0000ff9f;
  }
  &.high {
    background-color: #109618;
  }
}
</style>
