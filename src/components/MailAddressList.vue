<template>
  <div class="grouping">
    <input type="text" class="line-component email-to-add" placeholder="Email address" v-model.trim="email"></input>
    <email-add-btn class="line-component" v-bind:title="title" v-on:email-add-click="addEmailAddress"></email-add-btn>
    <email-removable-label class="line-component" v-for="address in addressList" v-bind:value="address.value" v-bind:key="address.key"></email-removable-label>
  </div>
</template>


<script>
import EmailAddBtn from './EmailAddBtn'
import EmailRemovableLabel from './EmailRemovableLabel'

export default {
  name: 'mail-address-list',
  components: {
    EmailAddBtn,
    EmailRemovableLabel
  },
  props: {
    title: null,
    addressList: []
  },
  methods: {
    addEmailAddress: function () {
      alert('Email add clicked: ' + this.email)
    }
  }
}
</script>


<style scoped>

.line-component{
  padding: 0.5em;
  float: left;
  margin-right: 0.5em;
}

.email-to-add {
  border-radius: 5px;
  padding: 0em;
  width: 15em;
}


</style>
