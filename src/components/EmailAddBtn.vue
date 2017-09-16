<template>
  <button class="btn btn-info badge badge-info title" v-on:click="fireEvent">
    <span class="fa fa-plus"></span>
    {{title}}
  </button>
</template>

<script>
export default {
  name: 'email-add-btn',
  props: {
    title: null
  },
  methods: {
    fireEvent: function () {
      this.$emit('email-add-click')
    }

  }
}
</script>

<style scoped>
.title {
  width: 5em;
  height: 100%;
}
.title:hover {
  cursor: pointer;
}
</style>
