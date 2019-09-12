<template>
  <div>
    <h1><center>{{monthName}}</center></h1>
  <v-simple-table style="height:100%;">
    <thead>
      <tr>
        <th class="text-left">Sunday</th>
        <th class="text-left">Monday</th>
        <th class="text-left">Tuesday</th>
        <th class="text-left">Wednesday</th>
        <th class="text-left">Thursday</th>
        <th class="text-left">Friday</th>
        <th class="text-left">Saturday</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="week in dishNightMonth">
        <td v-for="day in week">
          <v-card v-if="day.number != 'null'" color="yellow lighten-4">
            <v-card-title>
              {{ day.number}}
            </v-card-title>
            <v-card-text>
              {{day.name}}
            </v-card-text>
          </v-card>
        </td>
      </tr>
    </tbody>
  </v-simple-table>
  </div>
</template>

<script>

export default({
  name: 'dishNights',
  props: ['dishNightMonth', 'month'],
  data: () => ({

  }),
  mounted () {

  },
  computed: {
    monthName: function() {
      var months = ['January', 'Februrary', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
      return months[this.month - 1];
    }
  },
  methods: {

  }
});
</script>
