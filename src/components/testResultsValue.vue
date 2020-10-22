<template>
  <tr>
    <td>{{ testResultValue.name }}</td>
    <td>{{ testResultValue.date }}</td>
    <td>{{ testResultValue.score }}</td>
  </tr>
</template>

<script>
export default {
  name: "testResultsValue",

  props: {
    testResultValue: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
tr,
td {
  border: 1px solid rgb(200, 200, 200);
  text-align: center;
  padding: 1.5em;
}
</style>
