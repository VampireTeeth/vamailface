<template>
  <div>
    <b-form-input textarea
      v-model="text"
      placeholder="Say something here"
      v-on:blur="updateParent"
      :rows="10" :max-rows="20">
    </b-form-input>
  </div>
</template>

<script>
  export default {
    name: 'mail-text',
    data () {
      return {
        text: null
      }
    },

    methods: {
      updateParent: function () {
        this.$emit('input', this.text)
      }
    }
  }
</script>

<style scoped>
</style>
