<template>
  <span>{{ tableTop }}</span>
</template>
<script>
export default {
  name: 'TableTopHeader',
  props: {
    tableTop: {
      type: String,
      default: () => {
        return ''
      }
    }
  }
}
</script>
