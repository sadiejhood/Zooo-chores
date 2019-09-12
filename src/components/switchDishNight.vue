<template>
  <v-container>
    <v-layout
      text-left
      wrap
    >
    <v-flex>
      <v-card>
        <v-card-title> Change Dish Night </v-card-title>
        <v-card-text>
          Simply enter the date of the dish night you want to swith with your name and then the dish night you will be switching for and the other person's name. If there are questions, direct them to Sade please!
          <v-form>
            <v-text-field v-model="nameOne" label="Your Name"></v-text-field>
            <h2>Your dish night date!</h2>
            <v-date-picker landscape v-model="dateOne"></v-date-picker>
            <v-text-field v-model="nameTwo" label="Other Name"></v-text-field>
            <h2>The date of the other person's dish night!</h2>
            <v-date-picker landscape v-model="dateTwo"></v-date-picker>
            <v-btn v-on:click="flipNames">Change Dish Nights on Calendar!</v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-flex>
    </v-layout>
  </v-container>
</template>

<script>

export default ({
  name: 'switchDishNight',
  props: ['database', 'dishNights'],
  data: () => ({
    dateOne: new Date().toISOString().substr(0, 10),
    dateTwo: new Date().toISOString().substr(0, 10),
    nameOne: "",
    nameTwo: ""
  }),
  mounted () {

  },
  methods: {
    flipNames() {
      var firstDay = this.dateOne.substr(8)
      var secondDay = this.dateTwo.substr(8)

      if (this.dishNights.Assigned[firstDay - 1] === this.nameOne && this.dishNights.Assigned[secondDay - 1] === this.nameTwo) {

        this.dishNights.Assigned[firstDay - 1] = this.nameTwo
        this.dishNights.Assigned[secondDay - 1] = this.nameOne

        // call the db and update the array

        this.database.collection("dishNightMonth").doc("dishNightSeptember").update({Assigned: this.dishNights.Assigned})

      } else {
        alert("Whoops, one of those date:name combinations is incorrect")
      }
    }
  }
});
</script>
