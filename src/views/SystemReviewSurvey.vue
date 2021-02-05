<template>
  <v-row>
    <v-col cols="12" xs="12" sm="12" md="12" lg="6" xl="6" class="mx-auto">
      <v-stepper class="mx-auto" v-model="e6" vertical>
        <v-stepper-step :complete="e6 > 1" step="1" :editable="editable">
          Awardee
          <small>Awardee and Award information</small>
        </v-stepper-step>

        <v-stepper-content step="1">
          <v-card color="lime darken-5" class="mb-12" height="">
            <v-card-text class="mx-auto pa-10 text-center white--text">
              <h1 style="font-size: 32px; font-family: verdana">
                Franz Joshua A. Valencia
              </h1>
              <br />
              <cite style="font-size: 32px">Sunshine Award 2021</cite>
            </v-card-text>
          </v-card>
          <v-btn class="mb-2" color="primary" @click="e6 = 2">
            Start Survey
          </v-btn>
          <!-- <v-btn text> Cancel </v-btn> -->
        </v-stepper-content>

        <v-stepper-step :complete="e6 > 2" step="2" :editable="editable">
          Awardee Survey
          <small>Surveying the Awardee</small>
        </v-stepper-step>

        <v-stepper-content step="2">
          <!-- <v-card color="lime lighten-1" class="mb-12"> -->
          <AwardeeSurvey
            :is-cleared="isCleared"
            @dataChanged="dataChanged($event, 0)"
          />
          <!-- </v-card> -->
          <v-btn color="primary" @click="e6 = 3"> Continue </v-btn>
          <v-btn text @click="cancelSurvey"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-step :complete="e6 > 3" step="3" :editable="editable">
          System Review Survey I
          <small>Assessment of PRAISE Program</small>
        </v-stepper-step>

        <v-stepper-content step="3">
          <!-- <v-card color="lime lighten-1" class="mb-12"> -->
          <SystemReview1
            :is-cleared="isCleared"
            @dataChanged="dataChanged($event, 1)"
          />
          <!-- </v-card> -->
          <v-btn color="primary" @click="e6 = 4"> Continue </v-btn>
          <v-btn text @click="cancelSurvey"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-step :complete="e6 > 4" step="4" :editable="editable">
          System Review Survey II
          <small>Impact on Performance</small>
        </v-stepper-step>
        <v-stepper-content step="4">
          <!-- <v-card color="lime lighten-1" class="mb-12"> -->
          <SystemReview2
            :is-cleared="isCleared"
            @dataChanged="dataChanged($event, 2)"
            @cancelSurvey="cancelSurvey"
          />
          <!-- </v-card> -->
          <v-btn color="primary" @click="e6 = 5"> Continue </v-btn>
          <v-btn text @click="cancelSurvey"> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-step step="5" :editable="editable">
          Submit
          <small>Turn-in and restart survey</small>
        </v-stepper-step>
        <v-stepper-content step="5">
          <v-btn color="success" @click="turn_in">Submit</v-btn>
        </v-stepper-content>
      </v-stepper>
    </v-col>
  </v-row>
</template>
<script>
import AwardeeSurvey from "../components/rnr/survey/AwardeeSurvey";
import SystemReview1 from "../components/rnr/survey/SystemReview1";
import SystemReview2 from "../components/rnr/survey/SystemReview2";
export default {
  components: {
    AwardeeSurvey,
    SystemReview1,
    SystemReview2,
  },
  data() {
    return {
      e6: 1,
      isCleared: false,
      editable: true,
    };
  },
  methods: {
    dataChanged(event, survey) {
      if (survey == 0) {
        // this.e6 = 3;
        console.log(survey, event);
      } else if (survey == 1) {
        // this.e6 = 4;
        console.log(survey, event);
      } else if (survey == 2) {
        // this.e6 = 5;
        console.log(survey, event);
      }
    },
    cancelSurvey() {
      this.isCleared = true;
      setTimeout(() => {
        this.isCleared = false;
      }, 500);
      this.e6 = 1;
      // this.isCleared = false
    },
    turn_in() {
      this.cancelSurvey();
    },
  },
};
</script>