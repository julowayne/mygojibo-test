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
    <div class="container">
      <div id="person">
        <div><img src="../assets/welcome.svg" alt="" /></div>
        <div id="welcome">
          <div>Hi {{ firstname }} {{ lastname }}</div>
          <div>You can check your last results !</div>
        </div>
      </div>
      <globalResults
        v-if="testResults.length && stressDates.length && stressValues.length"
        :testResults="testResults"
        :stressDates="stressDates"
        :stressValues="stressValues"
      />
    </div>
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
          console.log(this.testResults);
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
    a {
      img {
        border-radius: 50%;
        width: 20%;
        height: 20%;
        box-shadow: $box-shadow-sm;
      }
    }
  }
}
#person {
  display: flex;
  text-align: left;
  #welcome {
    margin-top: 30px;
    font-size: 20px;
    letter-spacing: 1px;
    div:first-child {
      font-size: 30px;
      font-weight: bold;
      color: $teal;
    }
  }
  div {
    img {
      width: 100%;
    }
  }
}
</style>
