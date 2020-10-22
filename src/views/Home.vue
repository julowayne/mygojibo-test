<template>
  <div>
    <div id="person">
      <div>Name: {{ firstname }} {{ lastname }}</div>
      <div>status: {{ status }}</div>
    </div>
    <globalResults
      v-if="testResults.length && stressLevel.length"
      :testResults="testResults"
      :stressLevel="stressLevel"
    />
  </div>
</template>

<script>
import globalResults from "@/components/globalResults.vue";

export default {
  name: "HelloWorld",
  components: {
    globalResults
  },
  data: () => ({
    firstname: "",
    lastname: "",
    gender: 0,
    status: "",
    stressLevel: [],
    testResults: []
  }),
  methods: {
    fetchData() {
      fetch(`https://dev1-gojibrain.azurewebsites.net/testset`)
        .then(response => response.json())
        .then(data => {
          (this.firstname = data.firstname),
            (this.lastname = data.lastname),
            (this.gender = data.gender),
            (this.status = data.status),
            (this.stressLevel = data.stressLevel);
          this.testResults = data.testResults;
          console.log(data);
          console.log(this.stressLevel);
        });
    }
  },
  mounted() {
    this.fetchData();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
#person {
  display: flex;
  justify-content: center;
  flex-direction: column;
  height: 5vh;
  margin-top: 15px;
  font-size: larger;
}
</style>
