<template>
  <tr>
    <td>
      <img v-if="testResultValue" :src="nameImages" alt="name image" />
      {{ testResultValue.name }}
    </td>
    <td>{{ testResultValue.date }}</td>
    <td>
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
  color: $gray-600;
}
</style>
