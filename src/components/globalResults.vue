<template>
  <div id="results">
    <div class="chart-container">
      <canvas id="stress" width="400" height="400"></canvas>
    </div>
    <table>
      <thead>
        <tr>
          <th colspan="3">Stress Results</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Name</td>
          <td>Date</td>
          <td>Score</td>
        </tr>
        <testResultsValue
          v-for="(testResultValue, index) in testResults"
          :key="index"
          :testResultValue="testResultValue"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import Chart from "chart.js";

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
              backgroundColor: ["rgb(239,50,129, .7)"],
              borderColor: ["rgba(255, 255, 255)"],
              pointBackgroundColor: "rgba(235, 149, 50, 1)"
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
#results {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  padding: 0 10%;
  margin-top: 20px;
  height: 75vh;
  table {
    border-collapse: collapse;
    letter-spacing: 1px;
    font-family: sans-serif;
    font-size: 1rem;
    td {
      text-align: left;
      padding: 1.5rem;
    }
    tr {
      th {
        border: 1px solid lightgrey;
        padding: 1.5em;
        text-align: center;
        background-color: rgb(239, 50, 129, 0.5);
      }
      td {
        border: 1px solid rgb(200, 200, 200);
        background-color: rgb(239, 50, 129, 0.5);
        font-size: larger;
      }
    }
    td + td {
      margin-bottom: 20px;
    }
  }
  .chart-container {
    position: relative;
    height: 30vh;
    width: 35vw;
  }
}
</style>
