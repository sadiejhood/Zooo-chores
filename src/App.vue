<template>
  <v-app>
    <v-app-bar app color="teal lighten-3">
      <v-toolbar-title class="headline" v-on:click="changeMode(0)">
        <span>The Zooo Chore System</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-tabs
        right
        background-color="transparent"
      >
        <v-tab v-on:click="changeMode(1)">General Chores</v-tab>
        <v-tab v-on:click="changeMode(2)">Dish Night Schedule</v-tab>
        <v-tab v-on:click="changeMode(3)">Bathroom Clean Schedule</v-tab>
      </v-tabs>
    </v-app-bar>
    <v-content overflow>
      <Homepage v-if="mode === 'home'" v-bind:chores="EachHours"/>
      <DishNightPage v-if="mode === 'dish'" v-bind:dishNightMonth="tableValues" :month="dishNightMonth.Month"/>
      <SwitchDishNight v-if="mode === 'dish'" :database="database" :dishNights="dishNightMonth"/>
      <DishNightGenerator v-if="mode === 'dish'" :database="database" />
      <BathroomClean v-if="mode === 'bathroom'" :bathroomClean="bathroomClean"/>
      <genChore v-if="mode === 'gen'" :chores="chores"/>
    </v-content>
  </v-app>
</template>

<script>
import Homepage from './components/homepage';
import DishNightPage from './components/DishNightPage';
import BathroomClean from './components/BathroomCleanPage.vue';
import SwitchDishNight from './components/switchDishNight';
import genChore from './components/genChorePage.vue'
import DishNightGenerator from './components/dishNightGenerator.vue'

import * as firebase from "firebase/app";

import "firebase/auth";
import "firebase/firestore";
import "firebase/database"

var firebaseConfig = {
  apiKey: "AIzaSyDacgTxADV-Y2d6eC3-WgPxPh5s8fNN4z0",
  authDomain: "zooo-chores.firebaseapp.com",
  databaseURL: "https://zooo-chores.firebaseio.com",
  projectId: "zooo-chores",
  storageBucket: "zooo-chores.appspot.com",
  messagingSenderId: "70539295810",
};

firebase.initializeApp(firebaseConfig);
const database = firebase.firestore();

export default {
  name: 'App',
  components: {
    Homepage,
    DishNightPage,
    SwitchDishNight,
    BathroomClean,
    genChore,
    DishNightGenerator
  },
  data: () => ({
      chores: [

      ],
      EachHours: {
        oneHour: [],
        twoHours: [],
        threeHours: []
      },
      database: database,
      mode: "home",
      dishNightMonth: {},
      tableValues: [[],[],[],[],[]],
      bathroomClean: [
        [], [], []
      ]
    }),
    mounted () {
      this.getChores();
      this.getDishNights();
      this.getBathroomCleans();
    },
    methods: {
      getChores() {
        database.collection("chore").get()
            .then((element) => {
                element.forEach((doc) => {
                  if (doc.data().hours === 1){
                    this.EachHours.oneHour.push(doc.data())
                  } else if (doc.data().hours === 2){
                    this.EachHours.twoHours.push(doc.data())
                  } else if (doc.data().hours === 3){
                    this.EachHours.threeHours.push(doc.data())
                  }
                  this.chores.push(doc.data())
                })

                return element;
              });
        },
        getDishNights() {
          database.collection("dishNightMonth").get()
              .then((element) => {
                  element.forEach((doc) => {
                    var curDate = new Date()
                    console.log(curDate.getMonth())
                    console.log(doc.data().Month)
                    if (curDate.getMonth() + 1 === doc.data().Month) {
                      console.log(doc.data())
                      this.dishNightMonth = doc.data()
                      return doc.data();
                    }
                  })
                });
        },
        getBathroomCleans() {
          database.collection("bathroomClean").get()
              .then((element) => {
                  element.forEach((doc) => {
                    if (doc.id === "basement") {
                      doc.data().dates.forEach((date, index) => {
                        this.bathroomClean[0].push({date: new Date(date.seconds), name: doc.data().names[index]})
                      })
                    } else if (doc.id === "secondFloor") {
                      doc.data().dates.forEach((date, index) => {
                        this.bathroomClean[1].push({date: new Date(date.seconds), name: doc.data().names[index]})
                      })
                    } else if (doc.id === "thirdFloor") {
                      doc.data().dates.forEach((date, index) => {
                        this.bathroomClean[2].push({date: new Date(date.seconds), name: doc.data().names[index]})
                      })
                    }
                  })
                  return element;
                });
        },
        seperateDishNightInfo() {
          var currentName = 0;
          var namesRemain = true;
          var currentDay = 0;

          var curDate = new Date()

          for (var i = 0; i < this.dishNightMonth.firstDay; i++) {
            this.tableValues[0].push({
              number: "null",
              name: "null"
            });
          }

          for (var i = 0; i < 5; i++) {

            while ( this.tableValues[i].length < 7) {

              if (namesRemain) {
                currentDay += 1
                this.tableValues[i].push({
                  number: currentDay,
                  name: this.dishNightMonth.Assigned[currentName]
                });
                currentName += 1

                if (currentName > this.dishNightMonth.Assigned.length) {
                  namesRemain = false;
                }
              }
              else {

                if (this.daysInMonth(curDate.getYear(), this.dishNightMonth.Month) > currentDay) {
                  this.tableValues[i].push({
                    number: currentDay,
                    name: "null"
                  });
                  console.log(this.daysInMonth(curDate.getYear(), this.dishNightMonth.Month))
                  console.log(currentDay)
                }
                else {
                  this.tableValues[i].push({
                    number: "null",
                    name: "null"
                  });
                }

              }

            }
          }
        },
        daysInMonth(year, month) {
          return new Date(year, month, 0).getDate()
        },
        addNewChore() {
          let docRef = database.collection('chore').doc('HouseAccountant');

          let setAda = docRef.set({
            name: "House Accountant",
            possible_number_of_assigned_members: 1,
            hours: 3,
            description: "Takes care of finances, rent, etc. Keeps track of accounts for budgeting, etc. Has to have decent accounting and data management skills Trains next accountant in the spring or summer",
            assignees: [null]
          });
        },
        addDishNights() {
          let docRef = database.collection('dishNightMonth').doc('DishNightSept');

          let setAda = docRef.set({
            month: "September",
            year: 2019,
            firstDay: 0, //day of week //Sunday
            assignedDishNights: [
              "Sade", "Eli", "Bianca", "Nate", "David", "Greta", "Kristen", "San"
            ]
          });
        },
        changeMode(mode) {
          if (mode === 1) {
            this.mode = "gen"
          } else if (mode === 2) {
            this.seperateDishNightInfo()
            this.mode = "dish"
          } else if (mode === 3) {
            this.mode = "bathroom"
          } else {
            this.mode = "home"
          }
        }
    }
};
</script>

<style>

</style>
