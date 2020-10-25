<template>
  <div>
    <div id="header">
      <nav class="navbar navbar-light container">
        <a class="navbar-brand d-flex justify-content-start" href="#">
          Gojibo
        </a>
        <a class="d-flex justify-content-end" href=""
          ><img src="../assets/photo.jpg" alt="profil-picture"
        /></a>
      </nav>
    </div>
    <div id="person">
      Hi, {{ firstname }} {{ lastname }} you can check your last results !
      <div><img src="../assets/welcome.svg" alt="" /></div>
    </div>
    <globalResults
      v-if="testResults.length && stressDates.length && stressValues.length"
      :testResults="testResults"
      :stressDates="stressDates"
      :stressValues="stressValues"
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
    stressDates: [],
    stressValues: []
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
            (this.stressDates = data.stressLevel.map(stressLevel => {
              return stressLevel.date;
            }));
          this.stressValues = data.stressLevel.map(stressLevel => {
            return stressLevel.value;
          });
          console.log(data);
          console.log(this.stressDates);
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
#header {
  background-color: $teal;
  box-shadow: $box-shadow-sm;
  margin-bottom: $spacer * 3;
  nav {
    a:first-child {
      color: $white;
      font-size: xx-large;
    }
    img {
      margin-left: 20%;
      border-radius: 50%;
      width: 20%;
      height: 20%;
      box-shadow: $box-shadow-sm;
    }
  }
}
#person {
  img {
    width: 25%;
  }
}
</style>
