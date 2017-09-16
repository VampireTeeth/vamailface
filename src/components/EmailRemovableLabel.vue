<template>
  <span class="badge badge-success">
    <span class="fa fa-envelope"></span>
    {{value}}
    <button class="btn btn-success badge email-rm-btn">
      <span class="fa fa-remove"></span>
    </button>
  </span>
</template>

<script>
export default {
  name: 'email-removable-label',
  props: {
    value: null
  }
}
</script>

<style scoped>
.email-rm-btn:hover {
  cursor: pointer;
}
</style>
