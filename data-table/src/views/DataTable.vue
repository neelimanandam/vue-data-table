<template>
  <div>
    <data-table></data-table>
  </div>
</template>

<script>
// @ is an alias to /src
import DataTable from '@/components/DataTable.vue'

export default {
  name: 'DataTable',
  components: {
    DataTable
  }
}
</script>
