<template>
  <div id="results">
    <div class="chart-container">
      <canvas id="stress" width="400" height="400"></canvas>
    </div>
    <div class="tables-container">
      <table id="stress-result">
        <tbody>
          <tr id="headline">
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
      <table id="table-legend">
        <tbody>
          <tr>
            <td id="very-low">&lt; 25</td>
            <td>Very-low</td>
          </tr>
          <tr>
            <td id="low">25 &amp; 50</td>
            <td>Low</td>
          </tr>
          <tr>
            <td id="average">50 &amp; 75</td>
            <td>Average</td>
          </tr>
          <tr>
            <td id="high">&gt; 75</td>
            <td>High</td>
          </tr>
        </tbody>
      </table>
    </div>
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
  .chart-container {
    position: relative;
    height: 30vh;
    width: 35vw;
  }
  .tables-container {
    display: flex;
    justify-content: space-between;
    #stress-result {
      border-collapse: collapse;
      letter-spacing: 1px;
      font-family: sans-serif;
      font-size: 1rem;
      #headline {
        td {
          border: 1px solid rgb(200, 200, 200);
          font-weight: bold;
          background-color: rgb(220, 220, 220);
          font-size: larger;
          text-align: left;
        }
      }
      td {
        padding: 1.5rem;
      }
      td + td {
        margin-bottom: 20px;
      }
    }
    #table-legend {
      border-collapse: collapse;
      letter-spacing: 1px;
      font-family: sans-serif;
      font-size: 1rem;
      tr {
        td {
          td:first-child {
            color: white;
          }
          padding: 0.4rem 0.75rem;
        }
      }

      #very-low {
        background-color: #dc3a12f3;
      }
      #low {
        background-color: #ff9900;
      }
      #average {
        background-color: #109618;
      }
      #high {
        background-color: #0000ff;
      }
    }
  }
}
</style>
