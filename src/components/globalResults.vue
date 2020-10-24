<template>
  <div id="results">
    <div id="chart">
      <div id="chart-title">Stress level</div>
      <canvas
        id="stress"
        aria-label="Stress level line chart"
        role="chart"
      ></canvas>
    </div>
    <div id="stress-result">
      <div id="table-title">Stress results</div>
      <table class="table">
        <testResultsValue
          v-for="(testResultValue, index) in testResults"
          :key="index"
          :testResultValue="testResultValue"
        />
      </table>
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
      Chart.defaults.global.legend.display = false;
      var stressData = document.getElementById("stress").getContext("2d");
      // eslint-disable-next-line no-unused-vars
      var stress = new Chart(stressData, {
        type: "line",
        data: {
          labels: [
            dayjs(this.stressDates[0]).format("DD.MM"),
            dayjs(this.stressDates[1]).format("DD.MM"),
            dayjs(this.stressDates[2]).format("DD.MM"),
            dayjs(this.stressDates[3]).format("DD.MM"),
            dayjs(this.stressDates[4]).format("DD.MM"),
            dayjs(this.stressDates[5]).format("DD.MM"),
            dayjs(this.stressDates[6]).format("DD.MM"),
            dayjs(this.stressDates[7]).format("DD.MM"),
            dayjs(this.stressDates[8]).format("DD.MM"),
            dayjs(this.stressDates[9]).format("DD.MM"),
            dayjs(this.stressDates[10]).format("DD.MM"),
            dayjs(this.stressDates[11]).format("DD.MM")
          ],
          datasets: [
            {
              label: "Stress value",
              data: this.stressValues,
              backgroundColor: ["#20c997"],
              borderColor: ["#109618"],
              pointBackgroundColor: "rgba(235, 149, 50, 1)"
            }
          ]
        },
        options: {
          /*   label: {
            display: false
          },
          tooltips: {
            callbacks: {
              label: function(tooltipItem) {
                console.log(tooltipItem);
                return tooltipItem.yLabel;
              }
            }
          }, */
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
  #chart {
    background-color: $gray-100;
    padding: 1.5rem;
    border-radius: $border-radius;
    box-shadow: $box-shadow-sm;
    border: $border-color 1px solid;
    margin-bottom: 30px;
    margin: 0 10% 1% 10%;
    #chart-title {
      text-align: left;
      height: 5vh;
      margin: 0 0 1rem 1rem;
      font-size: x-large;
      color: $teal;
      padding: 0.5rem;
    }
  }
  #stress-result {
    background-color: $gray-100;
    letter-spacing: 1px;
    font-family: sans-serif;
    margin: 0 10% 10% 10%;
    padding: 1.5rem;
    border-radius: $border-radius;
    box-shadow: $box-shadow-sm;
    border: $border-color 1px solid;
    #table-title {
      text-align: left;
      height: 5vh;
      margin: 0 0 1rem 1rem;
      font-size: x-large;
      color: $teal;
      padding: 0.5rem;
    }
  }
}
</style>
