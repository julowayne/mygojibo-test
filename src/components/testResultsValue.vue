<template>
  <tr>
    <td>
      <img v-if="testResultValue" :src="nameImages" alt="name image" />
      {{ testResultValue.name }}
    </td>
    <td>{{ formatDate }}</td>
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
import dayjs from "dayjs";
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
      return dayjs(this.testResultValue.date).format("DD.MM");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "~bootstrap/scss/bootstrap";
td {
  padding: 0;
}
tr,
td {
  text-align: left;
  color: $gray-600;
  padding: 0;
  td:first-child {
    color: $black;
  }
  img {
    margin-right: 20px;
  }
}
</style>
