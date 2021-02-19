<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6" md="3">
        <v-text-field v-model="givenURL" label="Website URL"></v-text-field>
      </v-col>

      <v-col cols="12" sm="6" md="3">
        <v-btn primary color="Submit" @click="onSubmit"> Submit </v-btn>
      </v-col>

      <!-- <textarea v-model="fetchedJSON" rows="8" cols="40"></textarea> -->
      <pre > {{ fetchedJSON | pretty }} </pre> 
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",

  data: () => ({
    givenURL: "https://pathao.com/bn/" ,
    fetchedJSON: "{}",
  }),
  filters: {
    pretty: function (value) {
      return JSON.stringify(JSON.parse(value), null, 2);
    },
  },
  methods: {
    onSubmit() {
      console.log(this.givenURL);
      var finalURL =
        "http://localhost:3000/crawldata/" + encodeURIComponent(this.givenURL);

      console.log(finalURL);
      axios
        .get(finalURL, {})
        .then((response) => {
          console.log(response);
          this.fetchedJSON = JSON.stringify(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
};
</script>

<style scoped>

</style>