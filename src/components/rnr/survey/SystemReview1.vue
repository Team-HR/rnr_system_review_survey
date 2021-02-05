<template>
  <div>
    <v-container>
      <v-row>
        <v-col>
          <v-card class="mx-auto">
            <v-card-text>
              <v-form
                ref="form"
                lazy-validation
                @submit.prevent=""
              >
                <p>
                  Instructions: This survey will be used to improve our Rewards
                  & Recognition program. Please select your
                  corresponding choice.
                </p>

                <!-- <h3>I. Assessment of PRAISE Program</h3> -->

                <div v-for="(item, i) in items" :key="i">
                  <p>{{ item.qs }}</p>
                  <v-radio-group class="ml-10" v-model="answers[i].opt">
                    <v-radio
                      v-for="(opt, index) in item.opts"
                      :key="index"
                      :label="`${opt}`"
                      :value="opt"
                      hide-details
                    >
                    </v-radio>
                  </v-radio-group>
                  <v-text-field
                    v-if="answers[i].opt == 'Others, please specify:'"
                    v-model="answers[i].others"
                    outlined
                    hide-details
                    class="mb-5"
                    placeholder="Please specify here..."
                    full-width
                  ></v-text-field>
                </div>
                <!-- <v-btn color="primary" type="submit">Submit</v-btn>
                <v-btn type="cancel" @click="cancel_survey">Submit</v-btn> -->

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
  data() {
    return {
      items: [
        {
          qs: "a.  Is your work group excited about the recognition program?",
          opts: ["Yes", "No"],
        },
        {
          qs:
            "b.  Did the program describe how and why you should recognize others?",
          opts: ["Yes", "No"],
        },
        {
          qs: "c.  Are the program guidelines clear and communicated well?",
          opts: ["Yes", "No"],
        },
        {
          qs:
            "d.  Is the nomination and award process simple to use? (For Dept. Heads/Section Heads only)",
          opts: ["Yes", "No"],
        },
        {
          qs: "e.  How is it better than the previous program or activity?",
          opts: ["Poor", "Fair", "Good", "Excellent"],
        },
        {
          qs: "f.  What is the most exciting part of the process?",
          opts: ["Nomination", "Awarding", "Survey", "Others, please specify:"],
        },
        {
          qs: "g.  Are there areas for improvement?",
          opts: ["Yes", "No", "Others, please specify:"],
        },
        {
          qs:
            "h.  What trends do you prefer in how the PRAISE Committee deliver rewards and recognition?",
          opts: [
            "Monetary",
            "Growth or Learning Opportunities",
            "Plaques/Certificates",
            "Valuable experiences",
            "Others, please specify:",
          ],
        },
      ],
      answers: [
        { opt: "" },
        { opt: "" },
        { opt: "" },
        { opt: "" },
        { opt: "" },
        { opt: "", others: "" },
        { opt: "", others: "" },
        { opt: "", others: "" },
      ],
    };
  },

  watch:{
    isCleared: function (val){
        if (val) {
          this.answers.forEach((elemen) => {
            elemen.opt = ""
            if (elemen.others) {
              elemen.others = ""
            }
          });
        }
    },
     answers: {
      handler: function () {
        var answers = [];
        this.answers.forEach((element) => {
          if (element.opt == 'Others, please specify:') {
            answers.push(element.others);
          } else answers.push(element.opt);
        });
        this.$emit("dataChanged", answers);
      },
      deep: true,
    },
  },

  methods: {
    // submit_form() {
    //   // console.log(this.answers);
    //   var answers = [];
    //   this.answers.forEach((element) => {
    //     if (element.opt == "Others, please specify:") {
    //       answers.push(element.others);
    //     } else {
    //       answers.push(element.opt);
    //     }
    //   });
    //   // console.log(answers);
    //   this.$emit("dataChanged", answers);
    // },
    // cancel_survey() {
    //   this.$emit("cancelSurvey");
    // },
  },
};
</script>