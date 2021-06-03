<template>
  <div>
    <div>
      <slot name="header"> </slot>
    </div>

    <table id="table">
      <thead>
        <slot name="tableTop"></slot>

        <tr>
          <td colspan="100%">
            <table-top-header
              v-bind:tableTop="tableTopHeader"
            ></table-top-header>
          </td>
        </tr>
        <tr>
          <th v-for="header in headers" v-bind:key="header.index">
            <slot name="tableHeader" v-bind:item="header">
              <table-header v-bind:tableheader="header" />
            </slot>
          </th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(row, index) in rows" v-bind:key="index">
          <slot name="row" v-bind:item="row">
            <table-row v-bind:tablerow="row" v-bind:headerNames="headers">
            </table-row>
          </slot>
        </tr>

        <tr v-if="rows.length === 0">
          <td :colspan="headers.length">
            <slot name="noData"> No data found </slot>
          </td>
        </tr>
      </tbody>
    </table>
    <slot name="footer"></slot>
  </div>
</template>
<style>
#table {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
#table td,
#table th {
  border: 1px solid #ddd;
  padding: 8px;
}
#table th {
  color: rgb(2, 2, 2);
}
#table td {
  color: gray;
}
</style>
<script>
import TableHeader from './TableHeader.vue'
import TableRow from '@/components/TableRow.vue'
import TableTopHeader from './TableTopHeader.vue'

export default {
  components: { TableHeader, TableRow, TableTopHeader },
  name: 'DataTable',
  props: {
    headers: {
      type: Array,
      default: () => {
        return []
      }
    },
    rows: {
      type: Array,
      default: () => {
        return []
      }
    },
    tableTopHeader: {
      type: String,
      default: () => {
        return ''
      }
    }
  }
  // created: function () {
  //   console.log('tableTopHeader value is', this.tableTopHeader)
  // }
}
</script>
