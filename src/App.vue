<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <h1 class="mr-2">IHRIS</h1>
        <b>Rewards and Recognition <cite>Survey</cite></b>
      </div>

      <v-spacer></v-spacer>
      <!-- <v-btn color="success" :to="{path: 'system-review-survey'}" >system-review-surveys</v-btn> -->

      <router-link to="/system-review-survey" custom v-slot="{ navigate }">
        <v-btn class="mx-2" @click="navigate" color="success" role="link"><v-icon>mdi-pen</v-icon> System Review Survey</v-btn>
      </router-link>

      <router-link to="/system-review-survey-2" custom v-slot="{ navigate }">
        <v-btn @click="navigate" color="success" role="link"><v-icon>mdi-pen</v-icon> System Review Survey 2</v-btn>
      </router-link>
      
    </v-app-bar>

    <v-main>
      <v-container>
      <router-view></router-view>
      </v-container>
      
    </v-main>
  </v-app>
</template>

<script>


export default {
  name: "App",


  data: () => ({
    //
  }),
};
</script>
