<template>
  <div class="mail">
    <mail-address-list title="TO" v-bind:addressList="mailList" v-on:add-email="addTos"></mail-address-list>
    <mail-address-list title="CC" v-bind:addressList="mailList" v-on:add-email="addCcs"></mail-address-list>
    <mail-address-list title="BCC" v-bind:addressList="mailList" v-on:add-email="addBccs"></mail-address-list>
    <mail-subject v-model="subject"></mail-subject>
    <mail-text v-model="content"></mail-text>
    <div class="grouping"><b-button variant="success" v-on:click="sendMail">Send Mail</b-button></div>
  </div>
</template>


<script>
import MailSubject from './MailSubject'
import MailText from './MailText'
import MailAddressList from './MailAddressList'

export default {
  name: 'mail',
  components: {
    MailSubject, MailText, MailAddressList
  },
  methods: {
    sendMail: function () {
      alert('Send mail clicked! subject:' + this.subject + ', content: ' + this.content)
    },
    addTos: function (val) {
      alert('addTos: ' + val)
    },
    addCcs: function (val) {
      alert('addCcs: ' + val)
    },
    addBccs: function (val) {
      alert('addBccs: ' + val)
    }
  },
  data () {
    return {
      subject: null,
      content: null,
      mailList: [{value: 'aaa', key: 0}, {value: 'bbb', key: 1}, {value: 'ccc', key: 2}]
    }
  }
}
</script>
<style scoped>
div.mail {
  width: 80%;
  margin: 2em auto;
}
div.mail>div {
  margin-bottom: 2em;
}

div button.btn {
  float: left;
}
</style>
