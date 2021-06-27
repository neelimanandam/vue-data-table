<template>
  <div>
    <input
      type="text"
      v-bind="searchItem"
      placeholder="search here"
      size="75"
    />
  </div>
</template>
<script>
export default {
  name: 'SearchBarComponent',
  data () {
    return {
      searchItem: ''
    }
  },
  props: {
    filterableRows: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  created () {
    console.log('searched item is', this.searchItem)
    console.log('rows are', this.filteredRows)
  },
  computed: {
    filteredRows () {
      if (!this.searchItem) {
        return this.filterableRows
      } else {
        return this.filterableRows.filter(this.FilterBysearch)
      }
    }
  },
  methods: {
    FilterBysearch: function (value) {
      const searchElement = this.searchItem.toLowerCase()
      return value.text.toLowerCase().match(searchElement)
    }
  }
}
</script>
