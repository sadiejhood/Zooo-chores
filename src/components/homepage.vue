<template>
  <v-container>
    <v-layout
      text-left
      wrap
    >
    <v-flex>
      <v-card>
        <v-card-title>Welcome to the Zooo's new chore application</v-card-title>
        <v-card-text>
          <h3>What is this?</h3>
          <div>Basically this is a simple app that will hopefully assist members of the Zooo (and maybe future coops as well) in
            their day to day lives regarding chores and responsibilities</div>
        </v-card-text>
      </v-card>
      <v-spacer></v-spacer>
      <v-card>
        <v-card-title><strong>Our Current Chores</strong> </v-card-title>
          <v-card-text>
            <v-container fluid>
              <v-row>
                  <v-card class="yellow light-2">
                  <v-card-title> <strong>One Hour Chores</strong> </v-card-title>
                  <v-card-text>
                    <div v-for="chore in chores.oneHour">
                      <ChoreCard v-bind:chore="chore"></ChoreCard>
                    </div>
                  </v-card-text>
                  </v-card>
                  <v-card class="light-green light-2">
                  <v-card-title> <strong>Two Hour Chores</strong> </v-card-title>
                  <v-card-text>
                    <div v-for="chore in chores.twoHours">
                      <ChoreCard v-bind:chore="chore"></ChoreCard>
                    </div>
                  </v-card-text>
                  </v-card>
                  <v-card class="orange light-2">
                  <v-card-title> <strong>Three Hour Chores </strong></v-card-title>
                  <v-card-text>
                    <div v-for="chore in chores.threeHours">
                      <ChoreCard v-bind:chore="chore"></ChoreCard>
                    </div>
                  </v-card-text>
                </v-card>
            </v-row>
              </v-container>
              </v-card-text>
      </v-card>
    </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import ChoreCard from './choreCard.vue'
import DishNights from './DishNightPage.vue'


export default ({
  name: 'homepage',
  components:
  {
    ChoreCard: ChoreCard,
    DishNights: DishNights
  },
  props: ['chores'],
  data: () => ({

  }),
  mounted () {

  },
  methods: {

  }
});
</script>
