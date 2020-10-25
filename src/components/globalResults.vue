<template>
  <div id="results">
    <div id="chart">
      <div class="title">Stress level</div>
      <canvas
        id="stress"
        aria-label="Stress level line chart"
        role="chart"
      ></canvas>
    </div>
    <div id="stress-result">
      <div class="title">Stress results</div>
      <testResultsValue
        v-for="(testResultValue, index) in testResults"
        :key="index"
        :testResultValue="testResultValue"
      />
    </div>
  </div>
</template>

<script>
import Chart from "chart.js";
import dayjs from "dayjs";
import "bootstrap";
import "jquery";
import "popper.js";

import testResultsValue from "@/components/testResultsValue.vue";
export default {
  name: "GlobalResults",
  components: {
    testResultsValue
  },
  props: {
    stressDates: Array,
    stressValues: Array,
    testResults: Array
  },
  methods: {
    stressLine() {
      const chartDates = this.stressDates.map(date =>
        dayjs(date, "D/MM/YYYY").format("DD/MM")
      );
      console.log(chartDates);
      Chart.defaults.global.legend.display = false;
      var stressData = document.getElementById("stress").getContext("2d");
      // eslint-disable-next-line no-unused-vars
      var stress = new Chart(stressData, {
        type: "line",
        data: {
          labels: chartDates,
          datasets: [
            {
              label: "Stress value",
              data: this.stressValues,
              backgroundColor: "#20c997",
              pointBackgroundColor: "#498c6c"
            }
          ]
        },
        options: {
          scales: {
            yAxes: [
              {
                ticks: {
                  beginAtZero: true,
                  min: 0,
                  max: 100,
                  callback: function(value) {
                    return value + "%";
                  }
                }
              }
            ]
          }
        }
      });
    }
  },
  mounted() {
    this.stressLine();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "~bootstrap/scss/bootstrap";
#results {
  .title {
    text-align: left;
    height: 5vh;
    margin: 0 0 1rem 0;
    font-size: x-large;
    color: $teal;
  }
  #chart {
    background-color: $gray-100;
    padding: 1.5rem;
    border-radius: $border-radius;
    box-shadow: $box-shadow-sm;
    border: $border-color 1px solid;
    margin-bottom: 30px;
  }
  #stress-result {
    background-color: $gray-100;
    letter-spacing: 1px;
    font-family: sans-serif;
    padding: 1.5rem;
    border-radius: $border-radius;
    box-shadow: $box-shadow-sm;
    border: $border-color 1px solid;
  }
}
@media (max-width: 504px) {
  #results {
    .title {
      font-size: large;
    }
  }
}
</style>
