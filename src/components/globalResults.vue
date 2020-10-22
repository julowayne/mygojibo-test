<template>
  <div id="results">
    <table>
      <thead>
        <tr>
          <th colspan="2">Stress Level</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Date</td>
          <td>Value</td>
        </tr>
        <stressLevelValue
          v-for="(stressLevelValue, index) in stressLevel"
          :key="index"
          :stressLevelValue="stressLevelValue"
        />
      </tbody>
    </table>
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
import stressLevelValue from "@/components/stressLevelValue.vue";
import testResultsValue from "@/components/testResultsValue.vue";

export default {
  name: "GlobalResults",
  components: {
    stressLevelValue,
    testResultsValue
  },
  props: {
    stressLevel: Array,
    testResults: Array
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
        border-bottom: 1.5px solid grey;
        padding: 1.5em;
        text-align: center;
        background-color: rgb(220, 220, 220);
      }
      td {
        border: 1px solid rgb(200, 200, 200);
        border-bottom: 1.5px solid grey;
        background-color: rgb(220, 220, 220);
        font-size: larger;
      }
    }
    td + td {
      margin-bottom: 20px;
    }
  }
}
</style>
