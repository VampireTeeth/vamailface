<template>
  <div class="mail">
    <div><input placeholder="Subject" v-model="subject"></div>
    <div><textarea placeholder="Content" v-model="content"></textarea></div>
    <div><button v-on:click="sendMail">Send Mail</button></div>
  </div>
</template>

<script>
export default {
  name: 'mail',
  methods: {
    sendMail: function () {
      alert('Send mail clicked! subject:' + this.subject + ', content: ' + this.content)
    }
  },
  props: {
    subject: null,
    content: null
  }
}
</script>
<style>
</style>
