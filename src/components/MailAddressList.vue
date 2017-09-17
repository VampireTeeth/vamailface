<template>
  <div>
    <div class="grouping">
      <span class="badge badge-danger error-msg">{{errorMsg}}</span>
    </div>
    <div class="grouping">
      <input type="text" class="line-component email-to-add" placeholder="Email address" v-model.trim="email" v-on:keyup.enter="onEmailAddClick"></input>
      <email-add-btn class="line-component" v-bind:title="title" v-on:email-add-click="onEmailAddClick"></email-add-btn>
    </div>
    <div class="grouping">
      <email-removable-label class="line-component" v-for="address in addressList" v-bind:address="address" v-bind:key="address.key" v-on:email-rm-click="onEmailRmClick"></email-removable-label>
    </div>
  </div>
</template>


<script>
import EmailAddBtn from './EmailAddBtn'
import EmailRemovableLabel from './EmailRemovableLabel'

const emailRegex = /^([\w\d]+\.)*?[\w\d]+[\w\d]@([\w\d]+\.)*?[\w\d]+[\w\d]$/

export default {
  name: 'mail-address-list',
  components: {
    EmailAddBtn,
    EmailRemovableLabel
  },
  props: {
    title: null,
    addressList: {
      type: Array,
      default: []
    }
  },
  data () {
    return {
      email: null,
      errorMsg: null
    }
  },
  methods: {
    onEmailAddClick: function () {
      const grp = this.email.match(emailRegex)
      if (grp) {
        this.errorMsg = null
        this.$emit('add-email', this.email)
        this.email = null
      } else {
        this.errorMsg = 'Invalid email: ' + this.email
      }
    },
    onEmailRmClick: function (key) {
      this.$emit('rm-email', key)
    },
    setErrorMsg: function (msg) {
      this.errorMsg = msg
    }
  }
}
</script>


<style scoped>

.line-component{
  padding: 0.5em;
  float: left;
  margin-right: 0.5em;
  margin-bottom: 0.5em;
}

.email-to-add {
  border-radius: 5px;
  padding: 0em;
  width: 15em;
}
span.error-msg {
  display: inline-block;
  padding: 0em;
}


</style>
