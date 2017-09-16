<template>
  <div class="grouping">
    <button class="btn btn-success btn-send-mail" v-bind:disabled="isActive" v-on:click="fireEvent">
      <span class="fa fa-spinner" v-bind:class="{'fa-spin': isActive}"></span>
      Send Mail
    </button>
  </div>
</template>

<script>
export default {
  name: 'mail-send-btn',
  props: {
    isActive: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    fireEvent: function () {
      this.$emit('send-mail-click')
    }
  }
}
</script>

<style scoped>
.btn-send-mail:hover {
  cursor: pointer;
}
</style>
