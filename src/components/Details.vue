<template>
  <q-layout>
    <div id="formdiv">
      <div class="floating-label">
          <input v-model="name" required size="50">
          <label>Name</label>
      </div>
      <br />
      <div class="floating-label">
          <input v-model="emailId" required size="50">
          <label>EmailID</label>
      </div>
      <br />
      <div class="floating-label">
          <input v-model="contactNo" required size="40">
          <label>Contact No</label>
      </div>
      <div class="floating-label">
        <textarea v-model="sop" required class="full-width"></textarea>
        <label>Something about you</label>
      </div>
      <br /><br />
      <button class="primary" @click="SubmittedForm()">Submit</button>
    </div>
  </q-layout>
</template>
<script>
import axios from 'axios'
import { Dialog } from 'quasar'
export default {
  data () {
    return {
      name: '',
      emailId: '',
      contactNo: '',
      sop: ''
    }
  },
  methods: {
    SubmittedForm () {
      axios.post('https://recruitmentserver.herokuapp.com/application', {
        name: this.name,
        emailId: this.emailId,
        contactNo: this.contactNo,
        sop: this.sop
      })
      .then(function (response) {
        console.log(response)
        if (response.data === 'data not allowed') {
          Dialog.create({
            title: 'Alert',
            message: 'Thanks for applying.But sorry the position is taken'
          })
        }
        else {
          Dialog.create({
            title: 'Alert',
            message: 'Thanks for applying.Your application has been submitted and will be considered.You will be informed soon.'
          })
        }
      })
      .catch(function (error) {
        console.log(error)
      })
    }
  }
}
</script>
<style>
#formdiv {
  padding-left: 400px;
  padding-top: 10px;
},
#col1 {
  column-width: 100px;
}
</style>
