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
          <td colspan="100%">
            <input
              type="text"
              size="75"
              v-model="searchItem"
              placeholder="search here"
            />
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
        <tr v-for="(row, index) in filteredRows" v-bind:key="index">
          <slot name="row" v-bind:item="row">
            <table-row v-bind:tablerow="row" v-bind:headerNames="headers">
            </table-row>
          </slot>
        </tr>

        <tr v-if="filteredRows.length === 0">
          <td :colspan="headers.length">
            <slot name="noData"> No data found </slot>
          </td>
        </tr>
        <tr>
          <td :colspan="headers.length">
            <label for="rows">Rows per page:</label>
            <select
              name="rows"
              id="rows"
              v-model="dropDownListValue"
              v-on:change="dropDownValueChange"
            >
              <option value="5">5</option>
              <option value="10">10</option>
              <option value="15">15</option>
              <option value="20">20</option>
            </select>
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
#searchBar {
  text-align: left;
}
</style>
<script>
import TableHeader from './TableHeader.vue'
import TableRow from '@/components/TableRow.vue'
import TableTopHeader from './TableTopHeader.vue'

export default {
  components: { TableHeader, TableRow, TableTopHeader },
  name: 'DataTable',
  data () {
    return {
      searchItem: '',
      dropDownListValue: 5,
      tableRows: []
    }
  },
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
  },
  computed: {
    filteredRows () {
      if (!this.searchItem) {
        for (var i = 0; i < this.dropDownListValue; i++) {
          var trows = this.tableRows
          trows = trows + this.rows
          console.log(trows)
        }
        return this.rows
      } else {
        return this.rows.filter(this.FilterBysearch)
      }
    }
  },
  methods: {
    searchItemValue () {
      console.log('search item is', this.searchItem)
      this.searchItem = ''
    },
    FilterBysearch: function (value) {
      const searchElement = this.searchItem.toLowerCase()
      let found = false
      for (var i = 0; i < this.headers.length; i++) {
        if (value[this.headers[i]].toLowerCase().match(searchElement)) {
          console.log('inside if...')
          found = true
          console.log('inside if found', found)
        }
      }

      console.log('return value', found)
      return found
    },
    dropDownValueChange () {
      console.log('drop down value is', this.dropDownListValue)
    }
  }

  // created: function() {
  //   console.log('search message is', this.searchitem)
  // },
}
</script>
