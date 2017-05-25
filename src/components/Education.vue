<template>
  <q-layout>
    <div id="formdiv">
      <pre><q-select label="Year" type="list" v-model="yr" :options="yrOptions"></q-select>                    <q-select label="Year Of Joining" type="list" v-model="yrjn" :options="yrjnOptions" onmousedown="if(this.options.length>3){this.size=3;}"  onchange='this.size=0;' onblur="this.size=0;"></q-select></pre>
      <br />
      <q-select class="full-width" label="College" type="list" v-model="coll" :options="collOptions"></q-select>
      <form action = "/#/details">
        <pre>                   <button class="primary" @click="addEducation()">Next</button></pre>
      </form>
    </div>
  </q-layout>
</template>
<script>
import axios from 'axios'

export default {
  data () {
    return {
      yr: '1',
      coll: 'ssn',
      yrjn: '2011',
      collOptions: [],
      yrOptions: [
        {
          label: 'First',
          value: '1'
        },
        {
          label: 'Second',
          value: '2'
        },
        {
          label: 'Third',
          value: '3'
        },
        {
          label: 'Fourth',
          value: '4'
        },
        {
          label: 'Fifth',
          value: '5'
        }
      ],
      yrjnOptions: [
        {
          label: '2011',
          value: '2011'
        },
        {
          label: '2012',
          value: '2012'
        },
        {
          label: '2013',
          value: '2013'
        },
        {
          label: '2014',
          value: '2014'
        },
        {
          label: '2015',
          value: '2015'
        },
        {
          label: '2016',
          value: '2016'
        },
        {
          label: '2017',
          value: '2017'
        }
      ]
    }
  },
  methods: {
    addEducation () {
      axios.post('https://recruitmentserver.herokuapp.com/temp', {
        year: this.yr,
        yearOfJoining: this.yrjn,
        college: this.coll
      })
      .then(function (response) {
      //  console.log(response)
      })
      .catch(function (error) {
        console.log(error)
      })
    }
  },
  mounted () {
    var xyz = this
    axios.get('https://recruitmentserver.herokuapp.com/college')
      .then(function (response) {
        var r
        for (r in response.data) {
          console.log(response.data[r].college)
          var obj = {
            'label': response.data[r].college,
            'value': response.data[r].college
          }
          console.log(obj)
          xyz.collOptions.push(obj)
        }
      })
      .catch(function (error) {
        console.log(error)
      })
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
