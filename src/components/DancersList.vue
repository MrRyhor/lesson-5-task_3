<template>
  <div class="container" :class="{'blue': name.isActive}" @click = "$emit('add', name)">
    {{ name.name }}
  </div>
</template>
<script>
export default {
  name: "DancersList",

  props: {
    name: {
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
.blue {
    border: 2px solid blue;
    padding: 3px 5px;
}
</style>
