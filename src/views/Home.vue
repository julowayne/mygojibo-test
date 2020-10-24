<template>
  <div>
    <header class="shadow-sm">
      <div id="title">Gojibo</div>
      <div id="account">
        <div id="person">Hi, {{ firstname }} {{ lastname }}</div>
        <div id="img">
          <a href=""><img src="../assets/photo.jpg" alt="profil-picture"/></a>
        </div>
      </div>
      <!-- <div id="img"><img src="../assets/photo.jpg" alt="profil-picture" /></div> -->
    </header>
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
import "bootstrap";
import "jquery";
import "popper.js";

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
@import "~bootstrap/scss/bootstrap";
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 10vh;
  background-color: $teal;
  box-shadow: 0 2px 3px -3px black;
  margin-bottom: 30px;
  #account {
    display: flex;
    align-items: center;
    color: $white;
    #person {
      font-size: x-large;
    }
    #img {
      img {
        margin-left: 20%;
        border-radius: 50%;
        width: 20%;
        height: 20%;
        border: $white 1px solid;
      }
    }
  }
  #title {
    margin-left: 5%;
    font-size: 40px;
    color: $white;
  }
}
</style>
