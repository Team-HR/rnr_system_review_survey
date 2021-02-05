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

                <v-simple-table dense>
                  <template v-slot:default>
                    <thead>
                      <tr>
                        <th class="text-left"></th>
                        <th class="text-center">
                          <b>Poor</b>
                        </th>
                        <th class="text-center">
                          <b>Unsatisfactory</b>
                        </th>
                        <th class="text-center">
                          <b>Satisfactory</b>
                        </th>
                        <th class="text-center">
                          <b>Very Satisfactory</b>
                        </th>
                        <th class="text-center">
                          <b>Outstanding</b>
                        </th>
                        <th class="text-center">Rating</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="(question, i) in questions" :key="i">
                        <td>{{ question.qs }}</td>
                        <!-- <td colspan="5">
                          <v-slider 
                            step="25"
                            ticks="always"
                            tick-size="3"
                          />
                        </td> -->
                        <td class="text-center">
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
                        <td class="text-center">
                          <b>{{ question.pts }}</b
                          >/5
                        </td>
                      </tr>
                      <tr>
                        <td colspan="6" class="text-right">Overall Score:</td>
                        <td class="text-center">
                          <b>{{ overall_score }}</b
                          >/60
                        </td>
                      </tr>
                    </tbody>
                  </template>
                </v-simple-table>

                <p>
                  How does the employee/unit showcase any of the following
                  attributes: creativity, innovativeness, efficiency, integrity,
                  productivity, heroic deeds, exemplary behavior, extraordinary
                  acts and other personal efforts which contribute to the
                  efficiency, economy and improvement in government operations?
                </p>

                <v-textarea label="Answer:" outlined v-model="essay1" />

                <p>
                  Please identify outstanding accomplishments and best practices
                  that the awardee continously have?
                </p>

                <v-textarea label="Answer:" outlined v-model="essay2" />

                <!-- <v-btn color="success" type="submit">Next</v-btn> -->
                <!-- <v-btn class="mr-5" color="primary"> Continue </v-btn>

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
/**
 * component
 * data
 * data to store
 * store to ajax
 */

export default {
  props: {
    isCleared: Boolean,
  },
  data: () => ({
    valid: true,
    questions: [
      { qs: "Attitude towards work", pts: 1 },
      { qs: "Attitude to colleague", pts: 1 },
      { qs: "Attitude towards client", pts: 1 },
      { qs: "Commitment to public interest", pts: 1 },
      { qs: "Dedication at work", pts: 1 },
      { qs: "Initiative at work", pts: 1 },
      { qs: "Honesty on dealings with customers", pts: 1 },
      { qs: "Politeness", pts: 1 },
      { qs: "Ability to handle stressful situation", pts: 1 },
      { qs: "Attendance", pts: 1 },
      { qs: "Productivity", pts: 1 },
      { qs: "Creativity & Innovativeness", pts: 1 },
    ],
    essay1: "",
    essay2: "",
  }),

  watch: {
    isCleared: function (val) {
      if (val) {
        this.questions.forEach((elemen) => {
          elemen.pts = 1;
        });
        this.essay1 = "";
        this.essay2 = "";
      }
    },
    questions: {
      handler: function () {
        var answers = [];
        this.questions.forEach((element) => {
          answers.push(element.pts);
        });
        answers.push(this.essay1);
        answers.push(this.essay2);
        this.$emit("dataChanged", answers);
      },
      deep: true,
    },
    essay1: function() {
      var answers = [];
        this.questions.forEach((element) => {
          answers.push(element.pts);
        });
        answers.push(this.essay1);
        answers.push(this.essay2);
        this.$emit("dataChanged", answers);
    },
    essay2: function() {
      var answers = [];
        this.questions.forEach((element) => {
          answers.push(element.pts);
        });
        answers.push(this.essay1);
        answers.push(this.essay2);
        this.$emit("dataChanged", answers);
    }
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
    // next_survey() {
    //   var answers = [];
    //   this.questions.forEach((element) => {
    //     answers.push(element.pts);
    //   });
    //   answers.push(this.essay1);
    //   answers.push(this.essay2);
    //   this.$emit("dataChanged", answers);
    // },
    // cancel_survey() {
    //   this.$emit("cancelSurvey");
    // },
    set_pts(i, n) {
      this.questions[i].pts = n;
    },
  },
};
</script>