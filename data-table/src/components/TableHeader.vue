<template>
  <div>{{ tableheader }}</div>
</template>

<script>
export default {
  name: 'TableHeader',
  props: {
    tableheader: {
      type: String,
      default: () => {
        return ''
      }
    }
  }
}
</script>
