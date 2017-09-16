<template>
  <div>
    <span class="badge badge-danger">{{errorMsg}}</span>
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
        value: null,
        errorMsg: null
      }
    },
    methods: {
      updateParent: function () {
        this.setErrorMsg(null)
        this.$emit('input', this.value)
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
  padding: 0;
}
</style>

<!-- form-input-1.vue -->
