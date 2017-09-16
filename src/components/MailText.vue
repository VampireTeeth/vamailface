<template>
  <div>
    <span class="badge badge-danger">{{errorMsg}}</span>
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
        text: null,
        errorMsg: null
      }
    },

    methods: {
      updateParent: function () {
        this.setErrorMsg(null)
        this.$emit('input', this.text)
      },
      setErrorMsg: function (msg) {
        this.errorMsg = msg
      }
    }
  }
</script>

<style scoped>
.badge-danger {
  display:inline-block;
  padding: 0
}
</style>
