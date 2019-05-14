<template>
  <v-stepper v-model="e6" vertical>
    <v-stepper-step :complete="e6 > 1" step="1">
        Getting Candidates
        <small>Via AddressService, LandmarkService, DictionaryService</small>
    </v-stepper-step>

    <v-stepper-content step="1">
      <v-card color="grey lighten-1" class="mb-5">
        <Candidate :steps="result._steps"/>
      </v-card>
      <v-btn color="primary" @click="e6 = 2">Continue</v-btn>
    </v-stepper-content>

    <v-stepper-step :complete="e6 > 2" step="2">
        Finding Search Pattern
        <small>Via PatternBuilder</small> 
    </v-stepper-step>

    <v-stepper-content step="2">
      <v-card color="grey lighten-1" class="mb-5" height="300px">
        <PatternBuilder :result="result._steps.PatternBuilder.data"/>
      </v-card>
      <v-btn color="primary" @click="e6 = 3">Continue</v-btn>
      <v-btn flat @click="e6 = 1">Back</v-btn>
    </v-stepper-content>

    <v-stepper-step step="3">
        Completed
        <small>Via PatternExecutor, Let's check the results</small>
    </v-stepper-step>

    <v-stepper-content step="3">
      <v-card color="grey lighten-1" class="mb-5" height="600px">
        <Result :result="result"/>
      </v-card>
      <v-btn color="primary" @click="e6 = 1">Continue</v-btn>
      <v-btn flat @click="e6 = 2">Back</v-btn>
    </v-stepper-content>
  </v-stepper>
</template>

<script>
import Candidate from './Candidate'
import PatternBuilder from './PatternBuilder'
import Result from './Result'

export default {
  name: 'Step',
  props: ['result', 'keyword'],
  components: {
    Candidate, 
    PatternBuilder,
    Result
  },
  data () {
    return {
      e6: 1,
      keywordStep:''
    }
  },
  mounted() {
    console.log('step created')
    console.log(this.result)
    this.e6=1


  },
  updated() {
    if(this.keyword !== this.keywordStep){
      this.e6=1;
      this.keywordStep = this.keyword
    }
  }
}
        
</script>