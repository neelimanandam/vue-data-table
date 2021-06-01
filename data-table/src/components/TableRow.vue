<template>
  <div style="display: contents">
    <td v-for="(headerName, index) in headerNames" v-bind:key="index">
      {{ tablerow[headerName] }}
    </td>
  </div>
</template>
<script>
export default {
  name: 'TableRow',
  props: {
    tablerow: {
      type: Object,
      default: () => {
        return {}
      }
    },
    headerNames: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  mounted () {
    console.log(this.headerNames)
  }
}
</script>
