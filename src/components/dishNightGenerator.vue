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
          Simply enter a comma seperated list of all residents during the next month ({{ months[curDay.getMonth() + 1] }}) .
          <v-form>
            <v-text-field v-model="listOfResidents" label="List of Residents"></v-text-field>
            <v-btn v-on:click="generateNewCalendar">Change Dish Nights on Calendar!</v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-flex>
    </v-layout>
  </v-container>
</template>

<script>

export default ({
  name: 'DishNightGenerator',
  props: ['database'],
  data: () => ({
    listOfResidents: "",
    arrayOfResidents: [],
    dishNights: [],
    months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec'],
    curDay: new Date()
  }),
  mounted () {

  },
  methods: {
    shuffle(a) {
      var j, x, i;
      for (i = a.length - 1; i > 0; i--) {
          j = Math.floor(Math.random() * (i + 1));
          x = a[i];
          a[i] = a[j];
          a[j] = x;
      }
      return a;
    },
    getArray() {
      var arrayOfResidents = this.listOfResidents.split(',')
      this.arrayOfResidents = arrayOfResidents;
    },
    generateNewCalendar() {
      var curDate = new Date()

      this.getArray()
      this.arrayOfResidents = this.shuffle(this.arrayOfResidents)

      var i = 0

      while (this.dishNights.length < this.daysInMonth(curDate.getYear(), curDate.getMonth() + 1) || i < 20) {
        this.dishNights = this.dishNights.concat(this.shuffle(this.arrayOfResidents))
        i++;
      }
      this.dishNights = this.dishNights.slice(0, this.daysInMonth(curDate.getYear(), curDate.getMonth() + 1))

      this.addDishNights()
    },
    daysInMonth(year, month) {
      return new Date(year, month, 0).getDate()
    },
    addDishNights() {
      var docName = 'DishNight' + this.months[this.curDay.getMonth() + 1] + this.curDay.getYear().toString()
      this.database.collection('dishNightMonth')
      .doc(docName)
      .set({
        Month: this.curDay.getMonth() + 2,
        Year: this.curDay.getYear(),
        firstDay: 2, //day of week //Tuesday
        Assigned: this.dishNights
      });
    },
  }
});
</script>
