<template>
  <tr>
    <td>{{ stressLevelValue.date }}</td>
    <td>{{ stressLevelValue.value }}</td>
  </tr>
</template>

<script>
export default {
  name: "stressLevelValue",
  props: {
    stressLevelValue: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
tr,
td {
  border: 1px solid rgb(200, 200, 200);
  text-align: center;
  padding: 0.8em;
}
</style>
