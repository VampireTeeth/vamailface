<template>
  <div class="mail">
    <mail-subject v-model="subject"></mail-subject>
    <mail-text v-model="content"></mail-text>
    <div class="grouping"><b-button variant="success" v-on:click="sendMail">Send Mail</b-button></div>
  </div>
</template>


<script>
import MailSubject from './MailSubject'
import MailText from './MailText'

export default {
  name: 'mail',
  components: {
    MailSubject, MailText
  },
  methods: {
    sendMail: function () {
      alert('Send mail clicked! subject:' + this.subject + ', content: ' + this.content)
    }
  },
  data () {
    return {
      subject: null,
      content: null
    }
  }
}
</script>
<style>
div input.form-control,
div textarea.form-control{
  width: 80%;
  margin: 2em auto;
}
div button.btn {
  float: left;
  position: relative;
  left: 10%;
}
</style>
