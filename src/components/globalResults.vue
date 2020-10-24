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
        <tbody>
          <testResultsValue
            v-for="(testResultValue, index) in testResults"
            :key="index"
            :testResultValue="testResultValue"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Chart from "chart.js";
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
    dates: Array,
    values: Array,
    testResults: Array
  },
  methods: {
    stressLine() {
      var stressData = document.getElementById("stress").getContext("2d");
      // eslint-disable-next-line no-unused-vars
      var stress = new Chart(stressData, {
        type: "line",
        data: {
          labels: this.dates,
          datasets: [
            {
              label: "Stress value",
              data: this.values,
              backgroundColor: ["#20c997"],
              borderColor: ["#109618"],
              pointBackgroundColor: "rgba(235, 149, 50, 1)"
            }
          ]
        },
        options: {
          responsive: true,
          scales: {
            yAxes: [
              {
                ticks: {
                  fontColor: "$gray-600",
                  beginAtZero: true,
                  min: 0,
                  max: 100,
                  callback: function(value) {
                    return value + "%";
                  }
                }
              }
            ],
            xAxes: [
              {
                ticks: {
                  fontColor: "$gray-600"
                }
              }
            ]
          },
          legend: {
            display: false
          },
          tooltips: {
            callbacks: {
              label: function(tooltipItem) {
                return tooltipItem.yLabel;
              }
            }
          }
          /*    title: {
            display: true,
            text: "Stress level representation",
            fontSize: 15,
            fontColor: "$gray-600"
          }, */
          /*  layout: {
            padding: {
              left: 0,
              right: 200,
              top: 30,
              bottom: 30
            }
          } */
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
    /*   #stress {
      box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15) !important;
      margin-bottom: 40px;
    } */
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
