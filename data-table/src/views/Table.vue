<template>
  <div>
    <data-table
      v-bind:headers="userHeaders"
      v-bind:rows="userRows"
      v-bind:tableTopHeader="tableTopHeader"
    >
      <template v-slot:header>
        <h1>This is the header coming from slot</h1>
      </template>
      <template v-slot:footer>
        <h1>This footer is coming from slot</h1>
      </template>
      <!-- <template v-slot:tableTop>
        <span>This is table top</span>
      </template> -->
      <template v-slot:noData>
        <span>Data not found</span>
      </template>

      <template v-slot:row="{ item }">
        <td>
          <b>{{ item.country }}</b>
        </td>
        <td>
          <i>{{ item.state }}</i>
        </td>
        <td>
          <h2>{{ item.language }}</h2>
        </td>
      </template>
      <template v-slot:tableHeader="{ item }">
        <i>{{ item }} </i>
      </template>
    </data-table>
  </div>
</template>
<script>
import DataTable from '../components/DataTable.vue'
export default {
  name: 'Table',
  components: {
    DataTable
  },
  data () {
    return {
      tableTopHeader: 'This is the top of the table',
      userHeaders: ['country', 'state', 'language'],
      userRows: [
        { country: 'India', state: 'Telangana', language: 'Telugu' },
        { country: 'India', state: 'AP', language: 'Telugu' },
        { country: 'India', state: 'Tamil Nadu', language: 'Tamil' },
        { country: 'India', state: 'Bangalore', language: 'Kannada' }
      ]
    }
  }
}
</script>
