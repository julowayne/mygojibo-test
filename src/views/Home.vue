<template>
  <div>
    <div id="person">
      <div>Name: {{ firstname }} {{ lastname }}</div>
      <div>status: {{ status }}</div>
    </div>
    <globalResults
      v-if="testResults.length && dates.length && values.length"
      :testResults="testResults"
      :dates="dates"
      :values="values"
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
    testResults: [],
    dates: [],
    values: []
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
            (this.testResults = data.testResults),
            (this.dates = data.stressLevel.map(stressLevel => {
              return stressLevel.date;
            }));
          this.values = data.stressLevel.map(stressLevel => {
            return stressLevel.value;
          });
          console.log(data);
          console.log(this.dates);
          console.log(this.values);
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
  font-size: x-large;
}
</style>
