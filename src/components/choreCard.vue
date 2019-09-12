<template>
  <v-container>
    <v-layout
      text-left
      wrap
    >
    <v-flex>
      <v-card>
        <v-card-title>{{ chore.name }}</v-card-title>
        <v-card-text>
          Chore Hours: {{ chore.hours }} </br>
          Description: {{chore.description}}
        </v-card-text>
      </v-card>
    </v-flex>
    </v-layout>
  </v-container>
</template>

<script>

export default ({
  name: 'ChoreCard',
  props: ['chore'],
  data: () => ({

  }),
  mounted () {

  },
  methods: {

  }
});
</script>
