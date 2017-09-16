<template>
  <div class="mail">
    <mail-address-list title="TO" v-bind:addressList="tos" v-on:add-email="addTos" v-on:rm-email="rmTos"></mail-address-list>
    <mail-address-list title="CC" v-bind:addressList="ccs" v-on:add-email="addCcs"></mail-address-list>
    <mail-address-list title="BCC" v-bind:addressList="bccs" v-on:add-email="addBccs"></mail-address-list>
    <mail-subject v-model="subject"></mail-subject>
    <mail-text v-model="content"></mail-text>
    <mail-send-btn v-bind:isActive="isSendingEmail" v-on:send-mail-click="sendMail"></Mail-send-btn>
  </div>
</template>


<script>
import MailSubject from './MailSubject'
import MailText from './MailText'
import MailAddressList from './MailAddressList'
import MailSendBtn from './MailSendBtn'

var currentKey = 0

function filterByKeyOnEmailList (addressList, key) {
  return addressList.filter(function (addr) {
    return addr.key !== key
  })
}

function addToAddressList (addressList, email) {
  var nxtKey = ++currentKey
  addressList.push({value: email, key: nxtKey})
}

export default {
  name: 'mail',
  components: {
    MailSubject, MailText, MailAddressList, MailSendBtn
  },
  methods: {
    sendMail: function () {
      this.isSendingEmail = true
    },
    addTos: function (email) {
      addToAddressList(this.tos, email)
    },
    rmTos: function (key) {
      this.tos = filterByKeyOnEmailList(this.tos, key)
    },
    addCcs: function (email) {
      addToAddressList(this.ccs, email)
    },
    rmCcs: function (key) {
      this.ccs = filterByKeyOnEmailList(this.ccs, key)
    },
    addBccs: function (email) {
      addToAddressList(this.bccs, email)
    },
    rmBccs: function (key) {
      this.bccs = filterByKeyOnEmailList(this.bccs, key)
    }
  },
  data () {
    return {
      isSendingEmail: false,
      isSentEmail: false,
      sendMailMessage: 'SUCCESS',
      subject: null,
      content: null,
      tos: [],
      ccs: [],
      bccs: []
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
