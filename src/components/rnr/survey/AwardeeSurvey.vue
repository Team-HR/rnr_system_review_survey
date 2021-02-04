<template>
  <div>
    <v-container>
      <v-row>
        <v-col>
          <v-card class="mx-auto">
            <v-card-text>
              <v-form ref="form" v-model="valid" lazy-validation @submit.prevent="">
                <p>Please rate the awardee by clicking the stars based on the following standards:</p>
                <p>
                  <b>P</b> - Poor <b>US</b> - Unsatisfactory <b>S</b> -
                  Satisfactory <b>VS</b> - Very Satisfactory <b>O</b> -
                  Outstanding
                </p>

                <v-simple-table dense>
                  <template v-slot:default>
                    <thead>
                      <tr>
                        <th class="text-left"></th>
                        <th class="text-center">
                          <b>P</b>
                        </th>
                        <th class="text-center">
                          <b>US</b>
                        </th>
                        <th class="text-center">
                          <b>S</b>
                        </th>
                        <th class="text-center">
                          <b>VS</b>
                        </th>
                        <th class="text-center">
                          <b>O</b>
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
                          <b>{{ question.pts }}</b>/5
                        </td>
                      </tr>
                      <tr>
                        <td colspan="6" class="text-right">Overall Score:</td>
                        <td class="text-center">
                          <b>{{ overall_score }}</b>/60
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

                <v-textarea label="Answer:" outlined />

                <p>
                  Please identify outstanding accomplishments and best practices
                  that the awardee continously have?
                </p>

                <v-textarea label="Answer:" outlined />

                <!-- <v-btn color="success" type="submit">Next</v-btn> -->
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
  data: () => ({
    valid: true,
    awardee: "",
    award: "",
    questions: [
      { qs: "Attitude towards work", pts: 5 },
      { qs: "Attitude to colleague", pts: 5 },
      { qs: "Attitude towards client", pts: 5 },
      { qs: "Commitment to public interest", pts: 5 },
      { qs: "Dedication at work", pts: 5 },
      { qs: "Initiative at work", pts: 3 },
      { qs: "Honesty on dealings with customers", pts: 2 },
      { qs: "Politeness", pts: 5 },
      { qs: "Ability to handle stressful situation", pts: 4 },
      { qs: "Attendance", pts: 3 },
      { qs: "Productivity", pts: 2 },
      { qs: "Creativity & Innovativeness", pts: 3 },
    ],
  }),
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
    set_pts(i, n) {
      console.log(i, n);
      this.questions[i].pts = n;
    },
  },
};
</script>