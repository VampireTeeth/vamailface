<template>
  <div>
    <b-form-input type="text"
                  placeholder="Enter your subject"
                  v-model.trim="value"
                  v-on:blur="updateParent"></b-form-input>
  </div>
</template>

<script>
  export default {
    name: 'mail-subject',
    data () {
      return {
        value: null
      }
    },
    methods: {
      updateParent: function () {
        this.$emit('input', this.value)
      }
    }
  }
</script>

<style scoped>
</style>

<!-- form-input-1.vue -->
