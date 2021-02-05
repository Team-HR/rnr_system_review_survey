<template>
  <div>
    <v-container>
      <v-row>
        <v-col>
          <v-card class="mx-auto">
            <v-card-text>
              <v-form
                ref="form"
                v-model="valid"
                lazy-validation
                @submit.prevent=""
              >
                <p>
                  Please rate the awardee by clicking the stars based on the
                  following standards:
                </p>
                <!-- <p>
                  <b>P</b> - Poor <b>US</b> - Unsatisfactory <b>S</b> -
                  Satisfactory <b>VS</b> - Very Satisfactory <b>O</b> -
                  Outstanding
                </p> -->

                <v-simple-table dense class="mb-5">
                  <template v-slot:default>
                    <thead>
                      <tr>
                        <th class="text-left"></th>
                        <th class="text-center">
                          <b>Unsatisfactory</b>
                        </th>
                        <th class="text-center">
                          <b>Needs Improvement</b>
                        </th>
                        <th class="text-center">
                          <b>Meets Expectation</b>
                        </th>
                        <th class="text-center">
                          <b>Exceeds Expectation</b>
                        </th>
                        <th class="text-center">
                          <b>Exceptional</b>
                        </th>
                      </tr>
                    </thead>
                    <tbody>
                      <!-- 1,7,8,14 -->
                      <template v-for="(question, i) in questions">
                        <tr
                          v-if="i == 1 || i == 8"
                          :key="i"
                          class="grey lighten-3"
                        >
                          <td colspan="6">{{ question.qs }}</td>
                        </tr>
                        <tr v-else-if="i == 7 || i == 14" :key="i">
                          <td>{{ question.qs }}</td>
                          <td colspan="5">
                            <v-text-field
                              class="pt-5"
                              label="..."
                              outlined
                              v-model="questions[i].pts"
                            ></v-text-field>
                          </td>
                        </tr>
                        <tr v-else :key="i">
                          <td>{{ question.qs }}</td>
                          <!-- <td colspan="5">
                          <v-slider 
                            step="25"
                            ticks="always"
                            tick-size="3"
                          />
                        </td> -->
                          <td class="text-center">
                            <!-- :color="question.pts >= 1 ? 'warning' : ''" -->
                            <v-btn
                              :color="question.pts >= 1 ? 'warning' : ''"
                              icon
                              @click.prevent="set_pts(i, 1)"
                              ><v-icon>mdi-star-circle-outline</v-icon></v-btn
                            >
                          </td>
                          <td class="text-center">
                            <v-btn
                              :color="question.pts >= 2 ? 'warning' : ''"
                              icon
                              @click.prevent="set_pts(i, 2)"
                              ><v-icon>mdi-star-circle-outline</v-icon></v-btn
                            >
                          </td>
                          <td class="text-center">
                            <v-btn
                              :color="question.pts >= 3 ? 'warning' : ''"
                              icon
                              @click.prevent="set_pts(i, 3)"
                              ><v-icon>mdi-star-circle-outline</v-icon></v-btn
                            >
                          </td>
                          <td class="text-center">
                            <v-btn
                              :color="question.pts >= 4 ? 'warning' : ''"
                              icon
                              @click.prevent="set_pts(i, 4)"
                              ><v-icon>mdi-star-circle-outline</v-icon></v-btn
                            >
                          </td>
                          <td class="text-center">
                            <v-btn
                              :color="question.pts >= 5 ? 'warning' : ''"
                              icon
                              @click.prevent="set_pts(i, 5)"
                              ><v-icon>mdi-star-circle-outline</v-icon></v-btn
                            >
                          </td>
                        </tr>
                      </template>
                    </tbody>
                  </template>
                </v-simple-table>

                <!-- <v-btn class="mr-5" color="primary" type="submit">
                  Continue
                </v-btn>
                <v-btn @click="cancel_survey">Cancel</v-btn> -->
              </v-form>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  props: {
    isCleared: Boolean,
  },
  data: () => ({
    valid: true,
    questions: [
      {
        qs: "1. How does the employee's performance improve after the award?",
        pts: 1,
      },
      {
        qs: "2. Rate the following attributes",
      },
      { qs: "Dependability", pts: 1 },
      { qs: "Adaptability", pts: 1 },
      { qs: "Cooperativeness", pts: 1 },
      { qs: "Committed/Passionate", pts: 1 },
      { qs: "Proactive", pts: 1 },
      {
        qs: "Others, please specify:",
        pts: "",
      },
      // {
      //   qs: "3. What attributes has declined?",
      // },
      // { qs: "Dependability", pts: 2 },
      // { qs: "Adaptability", pts: 5 },
      // { qs: "Cooperativeness", pts: 4 },
      // { qs: "Committed/Passionate", pts: 3 },
      // { qs: "Proactive", pts: 2 },
      // {
      //   qs: "Others, please specify:",
      //   value: "",
      // },
    ],
  }),
  watch: {
    isCleared: function (val) {
      if (val) {
        this.questions.forEach((elemen, i) => {
          if (i != 1 ) {
            elemen.pts = i != 7?1:"";
          }
        });
      }
    },
    questions: {
      handler: function () {
        var answers = [];
        this.questions.forEach((element, i) => {
          if (i != 1) {
            answers.push(element.pts);
          }
        });
        this.$emit("dataChanged", answers);
      },
      deep: true,
    },
  },
  computed: {
    overall_score: function () {
      var totalPts = 0;
      this.questions.forEach((element) => {
        totalPts += element.pts;
      });
      return totalPts;
    },
  },

  methods: {
    color_grade: function () {
      var color = "grey";
      return color;
    },
    set_pts(i, n) {
      // console.log(i, n);
      this.questions[i].pts = n;
    },
    // submit_form() {
    //   var answers = [];
    //   this.questions.forEach((element) => {
    //     if (element.pts) {
    //       answers.push(element.pts);
    //     }
    //   });
    //   this.$emit("dataChanged", answers);
    //   // console.log(answers);
    // },
    // cancel_survey() {
    //   this.$emit("cancelSurvey");
    // },
  },
};
</script>