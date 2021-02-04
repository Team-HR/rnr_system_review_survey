<template>
  <v-row>
    <v-col cols="12" xs="12" sm="12" md="12" lg="6" xl="6" class="mx-auto">
      <v-stepper class="mx-auto" v-model="e6" vertical>
        <v-stepper-step :complete="e6 > 1" step="1" editable>
          Awardee
          <small>Awardee and Award information</small>
        </v-stepper-step>

        <v-stepper-content step="1">
          <v-card color="lime darken-5" class="mb-12" height="">

            <v-card-text class="mx-auto pa-10 text-center white--text">
              <h1 style="font-size: 32px; font-family: verdana">Franz Joshua A. Valencia</h1>
              <br>
              <cite style="font-size: 32px;">Sunshine Award 2021</cite>
            </v-card-text>

          </v-card>
          <v-btn class="mb-2"  color="primary" @click="e6 = 2"> Start Survey </v-btn>
          <!-- <v-btn text> Cancel </v-btn> -->
        </v-stepper-content>

        <v-stepper-step :complete="e6 > 2" step="2" editable>
          Awardee Survey
          <small>Surveying the Awardee</small>
        </v-stepper-step>

        <v-stepper-content step="2">
          <!-- <v-card color="lime lighten-1" class="mb-12"> -->
            <AwardeeSurvey />
          <!-- </v-card> -->
          <v-btn color="primary" @click="e6 = 3"> Continue </v-btn>
          <v-btn text> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-step :complete="e6 > 3" step="3" editable>
          System Review Survey I
          <small>Assessment of PRAISE Program</small>
        </v-stepper-step>

        <v-stepper-content step="3">
          <!-- <v-card color="lime lighten-1" class="mb-12"> -->
            <SystemReviewI />
          <!-- </v-card> -->
          <v-btn color="primary" @click="e6 = 4"> Continue </v-btn>
          <v-btn text> Cancel </v-btn>
        </v-stepper-content>

        <v-stepper-step step="4" editable>
          System Review Survey II
          <small>Impact on Performance</small>
        </v-stepper-step>
        <v-stepper-content step="4">
          <!-- <v-card color="lime lighten-1" class="mb-12"> -->
            <SystemReviewII />
          <!-- </v-card> -->
          <v-btn color="primary" @click="e6 = 1"> Submit </v-btn>
          <v-btn text> Cancel </v-btn>
        </v-stepper-content>
      </v-stepper>
    </v-col>
  </v-row>
</template>
<script>
import AwardeeSurvey from "../components/rnr/survey/AwardeeSurvey";
import SystemReviewI from "../components/rnr/survey/SystemReviewI";
import SystemReviewII from "../components/rnr/survey/SystemReviewII";
export default {
  components: {
    AwardeeSurvey,
    SystemReviewI,
    SystemReviewII
  },
  data() {
    return {
      e6: 1,
    };
  },
};
</script>