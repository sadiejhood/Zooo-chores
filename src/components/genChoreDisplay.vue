<template>
  <v-tooltip top dark color="black">
    <template v-slot:activator="{ on }">
      <div v-if="chore.name !== 'Cooking' && chore.name !== 'After Dinner Clean (AD Clean)'" v-on="on">
        <h2 id="h2">
          <center>{{chore.name}}</center>
        </h2>
        <v-simple-table>
          <thead>
          </thead>
          <tbody>
            <tr v-for="assignee in chore.assignees">
              <td v-if="assignee !== null" id="td">
                {{ assignee }}
              </td>
              <td v-else id="td">
                Unassigned
              </td>
            </tr>
          </tbody>
        </v-simple-table>
      </div>
      <div v-else v-on="on">
        <h2 id="h2">
          <center>{{chore.name}}</center>
        </h2>
        <v-simple-table>
          <thead>
            <tr>
              <th id="th">Sunday</th>
              <th id="th">Monday</th>
              <th id="th">Tuesday</th>
              <th id="th">Wednesday</th>
              <th id="th">Thursday</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td id="td">
                {{chore.sunday[0]}}
              </td>
              <td id="td">
                {{chore.monday[0]}}
              </td>
              <td id="td">
                {{chore.tuesday[0]}}
              </td>
              <td id="td">
                {{chore.wednesday[0]}}
              </td>
              <td id="td">
                {{chore.thursday[0]}}
              </td>
            </tr>
            <tr v-if="chore.name === 'Cooking'">
              <td id="td">
                {{chore.sunday[1]}}
              </td>
              <td id="td">
                {{chore.monday[1]}}
              </td>
              <td id="td">
                {{chore.tuesday[1]}}
              </td>
              <td id="td">
                {{chore.wednesday[1]}}
              </td>
              <td id="td">
                {{chore.thursday[1]}}
              </td>
            </tr>
          </tbody>
        </v-simple-table>
      </div>
    </template>
    <span>{{chore.description}}</span>
  </v-tooltip>
</template>

<script>

export default({
  name: 'dishNights',
  props: ['chore'],
  data: () => ({
    on: false
  }),
  mounted () {

  },
  computed: {

  },
  methods: {

  }
});
</script>

<style>
  #td {
    text-align: center;
    border: 1px solid lightgrey;
    background-color: #4091d2;
    color: black;
  }
  #th {
    background-color: #40e2ca;
    color: black;
  }
  #h2 {
    background-color: #40d281;
    border:1px solid lightgrey;
  }
</style>
