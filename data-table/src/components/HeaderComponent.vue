<template>
  <h1>{{ tableTopHeader }}</h1>
</template>
<script>
export default {
  name: 'HeaderComponent',
  props: {
    tableTopHeader: {
      type: String,
      default: () => {
        return ''
      }
    }
  }
}
</script>
