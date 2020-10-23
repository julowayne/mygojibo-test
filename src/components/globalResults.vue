<template>
  <div id="results">
    <div id="chart">
      <canvas
        id="stress"
        aria-label="Stress level line chart"
        role="chart"
      ></canvas>
    </div>
    <div class="table-title">Stress Results</div>
    <div class="tables-container">
      <table id="stress-result" class="table container mt-6">
        <tbody>
          <tr id="headline">
            <th scope="col">Name</th>
            <th scope="col">Date</th>
            <th scope="col">Score</th>
          </tr>
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
          title: {
            display: true,
            text: "Stress level representation",
            fontSize: 15,
            fontColor: "$gray-200"
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
@import "~bootstrap/scss/bootstrap";
#results {
  margin-top: 20px;
  #chart {
    padding: 0 10%;
    #stress {
      box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15) !important;
      margin-bottom: 40px;
    }
  }
  hr {
    width: 30%;
  }
  .table-title {
    height: 5vh;
    margin-top: 15px;
    font-size: x-large;
    color: $gray-600;
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
      box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
      #headline {
        text-align: left;
        color: $gray-700;
        td {
          font-weight: bold;
          background-color: rgb(220, 220, 220);
          font-size: larger;
          text-align: left;
        }
      }
    }
    #table-legend {
      border-collapse: collapse;
      letter-spacing: 1px;
      font-family: sans-serif;
      font-size: 1rem;
      margin-left: 50px;
      box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
      tr {
        td {
          padding: 0.4rem 0.75rem;
        }
      }
      td:first-child {
        color: white;
      }
      #very-low {
        background-color: #dc3a12f3;
      }
      #low {
        background-color: #ff9900;
      }
      #average {
        background-color: #0000ff9f;
      }
      #high {
        background-color: #109618;
      }
    }
  }
}
</style>
