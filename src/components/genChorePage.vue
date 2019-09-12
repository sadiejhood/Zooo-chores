<template>
  <v-container class="grey lighten-5">
    <h1><center>General Chore Page</center></h1>
    <v-row no-gutters class="mb-10" v-for="i in 8">
        <template v-for="(chore, n) in chores.slice(3 * (i - 1), 3 * (i))">
          <v-col :key="n">
            <genChoreDisplay :chore="chore"/>
          </v-col>
      </template>
    </v-row>
  </v-container>
</template>

<script>
import genChoreDisplay from './genChoreDisplay'

export default({
  name: 'genChore',
  props: ['chores'],
  components: {
    genChoreDisplay
  },
  data: () => ({

  }),
  mounted () {

  },
  computed: {

  },
  methods: {

  }
});
</script>
