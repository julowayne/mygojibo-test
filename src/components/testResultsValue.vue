<template>
  <tr>
    <td>{{ testResultValue.name }}</td>
    <td>{{ testResultValue.date }}</td>
    <td id="score" :class="scoreValue">{{ testResultValue.score }}</td>
  </tr>
</template>

<script>
export default {
  name: "testResultsValue",

  props: {
    testResultValue: Object
  },
  computed: {
    scoreValue() {
      if (
        this.testResultValue.score === "" ||
        this.testResultValue.score === ""
      )
        return null;
      else if (this.testResultValue.score < 25) return "very-low";
      else if (
        this.testResultValue.score >= 25 &&
        this.testResultValue.score < 50
      )
        return "low";
      else if (
        this.testResultValue.score >= 50 &&
        this.testResultValue.score < 75
      )
        return "average";

      return "high";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
tr,
td {
  border: 1px solid rgb(200, 200, 200);
  text-align: left;
  padding: 1em;
}
#score {
  padding: 1.5rem 2rem;
  background-color: #e9ecef;
  color: grey;
  &.very-low,
  &.low,
  &.average,
  &.high {
    color: white;
  }
  &.very-low {
    background-color: #dc3a12f3;
  }
  &.low {
    background-color: #ff9900;
  }
  &.average {
    background-color: #109618;
  }
  &.high {
    background-color: #0000ff;
  }
}
</style>
