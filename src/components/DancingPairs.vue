<template>
  <div class="container" @click="$emit('delete', dancingPairsList.id)">
    {{ dancingPairsList.pair }}
  </div>
</template>
<script>
export default {
  name: "DancingPairs",

  props: {
    dancingPairsList: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>
<style lang="css" scoped>
    .container {
        cursor: pointer;
    }
</style>
