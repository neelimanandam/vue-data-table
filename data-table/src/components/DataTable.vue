<template>
  <div>
    <div>
      <slot name="header">
        <header-component></header-component>
      </slot>
    </div>
    <table
      border="1px solid black;"
      style="border-collapse: collapse; text-align: center"
    >
      <thead>
        <slot name="tableTop"></slot>
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
table {
  border-collapse: "collapse";
  background-color: aqua;
}
</style>
<script>
import TableHeader from './TableHeader.vue'
import TableRow from '@/components/TableRow.vue'
import HeaderComponent from './HeaderComponent.vue'

export default {
  components: { TableHeader, TableRow, HeaderComponent },
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
    }
  }
  // created: function () {
  //   console.log(this.headers)
  // }
}
</script>
