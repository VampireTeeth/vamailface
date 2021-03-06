<template>
  <div class="mail">
    <mail-address-list ref="toAddressList" title="TO" v-bind:addressList="tos" v-on:add-email="addTos" v-on:rm-email="rmTos"></mail-address-list>
    <mail-address-list ref="ccAddressList" title="CC" v-bind:addressList="ccs" v-on:add-email="addCcs" v-on:rm-email="rmCcs"></mail-address-list>
    <mail-address-list ref="bccAddressList" title="BCC" v-bind:addressList="bccs" v-on:add-email="addBccs" v-on:rm-email="rmBccs"></mail-address-list>
    <mail-subject ref="mailSubject" v-model="subject"></mail-subject>
    <mail-text ref="mailText" v-model="content"></mail-text>
    <mail-send-btn v-bind:isActive="isSendingEmail()" v-on:send-mail-click="sendMail"></Mail-send-btn>
    <mail-info-modal v-if="isShowingInfoModal()" v-on:close="closeInfoModal()">
      <i slot="header" class="fa fa-2x" v-bind:class="[sendMailStatus.hasError ? 'fa-times' : 'fa-check']"></i>
      <span slot="body" v-bind:class="[sendMailStatus.hasError ? 'msg-error' : 'msg-success']">{{sendMailStatus.message}}</span>
    </mail-info-modal>
  </div>
</template>


<script>
import axios from 'axios'
import MailSubject from './MailSubject'
import MailText from './MailText'
import MailAddressList from './MailAddressList'
import MailSendBtn from './MailSendBtn'
import MailInfoModal from './MailInfoModal'

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

function validateAddressList (addressList, comp) {
  if (!addressList || addressList.length === 0) {
    comp.setErrorMsg('Required')
    return false
  }
  return true
}

function validateTextInput (txt, comp) {
  if (txt && (txt.trim() !== '')) return true
  comp.setErrorMsg('Required')
  return false
}

function validateAll (v) {
  var r1 = validateAddressList(v.tos, v.$refs.toAddressList)
  var r2 = validateTextInput(v.subject, v.$refs.mailSubject)
  var r3 = validateTextInput(v.content, v.$refs.mailText)
  return r1 && r2 && r3
}

function mkEmailList (addressList) {
  return addressList.map(function (addr) {
    return addr.value
  })
}

export default {
  name: 'mail',
  components: {
    MailSubject, MailText, MailAddressList, MailSendBtn, MailInfoModal
  },
  methods: {
    sendMail: function () {
      if (!validateAll(this)) return
      const st = this.sendMailStatus
      st.isSending = true
      axios.post('https://vamailteeth.herokuapp.com/mail',
        {
          tos: mkEmailList(this.tos),
          ccs: mkEmailList(this.ccs),
          bccs: mkEmailList(this.bccs),
          subject: this.subject,
          text: this.content
        }).then(function (resp) {
          st.hasError = resp.data.failed
          st.message = resp.data.message
          st.finished = true
        },
        function (err) {
          st.hasError = true
          st.message = 'Send Email Error: ' + err.message
          st.finished = true
        })
    },
    isSendingEmail: function () {
      return this.sendMailStatus.isSending
    },
    isShowingInfoModal: function () {
      const st = this.sendMailStatus
      return st.isSending && st.finished
    },
    closeInfoModal: function () {
      const st = this.sendMailStatus
      st.isSending = false
      st.finished = false
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
      sendMailStatus: {
        finished: false,
        isSending: false,
        hasError: false,
        message: 'SUCCESS'
      },
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
  margin-top: 0.5em;
  margin-bottom: 1em;
  padding: 0;
}

div button.btn {
  float: left;
}

.fa-times,
.fa-check {
  margin: 0 auto;
  padding: 0.3em 0.4em 0.3em 0.4em;
  border-radius: 50%;
  color: white;
}

.fa-times {
  background-color: #d9534f;
}

.fa-check {
  background-color: #5cb85c;
}
.msg-error {
  color: #d9534f;
}

.msg-success {
  color: #5cb85c;
}


</style>
