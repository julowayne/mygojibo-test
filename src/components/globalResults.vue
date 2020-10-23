<template>
  <div id="results">
    <div id="chart">
      <canvas
        id="stress"
        aria-label="Stress level line chart"
        role="chart"
      ></canvas>
    </div>
    <hr />
    <div class="table-title">Stress Results</div>
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
                  fontColor: "#000",
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
                  fontColor: "#000"
                }
              }
            ]
          },
          title: {
            display: true,
            text: "Stress level representation",
            fontSize: 20,
            fontColor: "#000"
          },
          layout: {
            padding: {
              left: 200,
              right: 200,
              top: 0,
              bottom: 50
            }
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
  margin-top: 20px;
  #chart {
    padding: 0 10%;
  }
  hr {
    width: 30%;
  }
  .table-title {
    height: 5vh;
    margin-top: 15px;
    font-size: x-large;
  }
  .tables-container {
    display: flex;
    justify-content: center;
    #stress-result {
      border-collapse: collapse;
      letter-spacing: 1px;
      font-family: sans-serif;
      font-size: 1rem;
      margin-bottom: 50px;
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
      margin-left: 50px;
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
