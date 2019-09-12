<template>
  <div>
    <h1><center>Bathroom Cleans</center></h1>
    <v-simple-table>
      <thead>
        <tr>
          <th><center>Basement</center></th>
          <th><center>Second Floor</center></th>
          <th><center>Third Floor</center></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="backgroundColor: lightgreen;">
            <v-simple-table>
              <thead>
                <tr>
                  <th class="text-left">Date</th>
                  <th class="text-left">Person</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="day in bathroomClean[0]">
                  <td>{{day.date.toString().substr(0, 11)}}</td>
                  <td>{{day.name}}</td>
                </tr>
              </tbody>
            </v-simple-table>
          </td>
          <td style="backgroundColor: lightgreen;">
            <v-simple-table>
              <thead>
                <tr>
                  <th class="text-left">Date</th>
                  <th class="text-left">Person</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="day in bathroomClean[1]">
                  <td>{{day.date.toString().substr(0, 11)}}</td>
                  <td>{{day.name}}</td>
                </tr>
              </tbody>
            </v-simple-table>
          </td>
          <td style="backgroundColor: lightgreen;">
            <v-simple-table>
              <thead>
                <tr>
                  <th class="text-left">Date</th>
                  <th class="text-left">Person</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="day in bathroomClean[2]">
                  <td>{{day.date.toString().substr(0, 11)}}</td>
                  <td>{{day.name}}</td>
                </tr>
              </tbody>
            </v-simple-table>
          </td>
        </tr>
      </tbody>
    </v-simple-table>
  </div>
</template>

<script>

export default({
  name: 'BathroomClean',
  props: ['bathroomClean'],
  data: () => ({

  }),
  computed: {

  },
  methods: {

  }
});
</script>
