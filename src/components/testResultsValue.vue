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
      else if (this.testResultValue.score < 20) return "very-low";
      else if (
        this.testResultValue.score >= 20 &&
        this.testResultValue.score < 40
      )
        return "low";
      else if (
        this.testResultValue.score >= 40 &&
        this.testResultValue.score < 60
      )
        return "average";
      else if (
        this.testResultValue.score >= 60 &&
        this.testResultValue.score < 80
      )
        return "high";

      return "very-high";
    }
  },
  mounted() {
    this.scoreValue();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
tr,
td {
  border: 1px solid rgb(200, 200, 200);
  text-align: center;
  padding: 1em;
}
#score {
  padding: 1.5rem 2rem;
  background-color: #e9ecef;
  color: grey;
  &.very-low,
  &.low,
  &.average,
  &.high,
  &.very-high {
    color: white;
  }
  &.very-low {
    background-color: #dc3a1251;
  }
  &.low {
    background-color: #ff9900;
  }
  &.average {
    background-color: #109618;
  }
  &.high {
    background-color: #00bfff;
  }
  &.very-high {
    background-color: #0000ff;
  }
}
</style>
