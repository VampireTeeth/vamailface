<template>
  <span class="badge badge-primary">
    <span class="fa fa-envelope"></span>
    {{address.value}}
    <button class="btn btn-danger badge email-rm-btn" v-on:click="fireEvent">
      <span class="fa fa-remove"></span>
    </button>
  </span>
</template>

<script>
export default {
  name: 'email-removable-label',
  props: {
    address: {
      type: Object,
      default: null
    }
  },
  methods: {
    fireEvent: function () {
      this.$emit('email-rm-click', this.address.key)
    }
  }
}
</script>

<style scoped>
.email-rm-btn:hover {
  cursor: pointer;
}
</style>
