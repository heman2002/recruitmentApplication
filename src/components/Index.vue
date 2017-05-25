<template>
  <q-layout>
    <div id="formdiv">
      <br />
      <q-select label="District" type="list" v-model="select" :options="selectOptions"></q-select>
      <div class="row group">
        <div class="column group">
          <small style="color:blue">Degree</small>
          <label>
            <q-radio v-model="degree" val="be" @input="isok='1'"></q-radio>
            B.E./B.Tech
          </label>
          <label>
            <q-radio v-model="degree" val="a&s" class="teal" @input="isok='2'"></q-radio>
            Arts and Science
          </label>
        </div>
          <div class="column group" v-if="isok === '1'">
            <small style="color:blue">Department</small>
            <label>
              <q-radio v-model="dept" val="cse"></q-radio>
              CSE
            </label>
            <label>
              <q-radio v-model="dept" val="it" class="teal"></q-radio>
              IT
            </label>
          </div>
          <div class="column group" v-if="isok === '2'">
            <small style="color:blue">Department</small>
            <label>
              <q-radio v-model="dept" val="bsc"></q-radio>
              bsc
            </label>
            <label>
              <q-radio v-model="dept" val="humanities" class="teal"></q-radio>
              humanities
            </label>
          </div>
        </div>
        <br /><br />
        <form action = "/#/education" method="get">
          <pre>                   <button class="primary" @click="CollegeDetails()">Next</button></pre>
        </form>
      </div>
  </q-layout>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      select: 'chennai',
      selectOptions: [
        {
          label: 'Chennai',
          value: 'chennai'
        },
        {
          label: 'Kanchipuram',
          value: 'kanchipuram'
        },
        {
          label: 'Thiruvallur',
          value: 'thiruvallur'
        }
      ],
      isok: '0',
      degree: '',
      dept: ''
    }
  },
  methods: {
    CollegeDetails () {
      axios.post('https://recruitmentserver.herokuapp.com/data', {
        district: this.select,
        degree: this.degree,
        department: this.dept
      })
      .then(function (response) {
        console.log(response)
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
