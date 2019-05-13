<template>
  <v-stepper v-model="e6" vertical>
    <v-stepper-step :complete="e6 > 1" step="1">
      Tokenizing keyword
      <small>Via AnalyzerService</small>
    </v-stepper-step>

    <v-stepper-content step="1">
      <v-card color="grey lighten-1" class="mb-5" height="200px"></v-card>
      <v-btn color="primary" @click="e6 = 2">Continue</v-btn>
      <v-btn flat>Cancel</v-btn>
    </v-stepper-content>

    <v-stepper-step :complete="e6 > 2" step="2">
        Getting Candidates
        <small>Via AddressService, LandmarkService, DictionaryService</small>
    </v-stepper-step>

    <v-stepper-content step="2">
      <v-card color="grey lighten-1" class="mb-5">
        <Candidate/>
      </v-card>
      <v-btn color="primary" @click="e6 = 3">Continue</v-btn>
      <v-btn flat>Cancel</v-btn>
    </v-stepper-content>

    <v-stepper-step :complete="e6 > 3" step="3">
        Finding Search Pattern
        <small>Via PatternBuilder</small> 
    </v-stepper-step>

    <v-stepper-content step="3">
      <v-card color="grey lighten-1" class="mb-5" height="200px"></v-card>
      <v-btn color="primary" @click="e6 = 4">Continue</v-btn>
      <v-btn flat>Cancel</v-btn>
    </v-stepper-content>

    <v-stepper-step :complete="e6 > 4" step="4">
        Executing builder
        <small>Via PatternExecutor</small>
    </v-stepper-step>

    <v-stepper-content step="4">
      <v-card color="grey lighten-1" class="mb-5" height="200px"></v-card>
      <v-btn color="primary" @click="e6 = 5">Continue</v-btn>
      <v-btn flat>Cancel</v-btn>
    </v-stepper-content>

    <v-stepper-step step="5">
        Completed
        <small>Let's check the results</small>
    </v-stepper-step>

    <v-stepper-content step="5">
      <v-card color="grey lighten-1" class="mb-5" height="600px">
        <Result/>
      </v-card>
      <v-btn color="primary" @click="e6 = 1">Continue</v-btn>
      <v-btn flat>Cancel</v-btn>
    </v-stepper-content>
  </v-stepper>
</template>

<script>
import Candidate from './Candidate'
import Result from './Result'

export default {
  name: 'Step',
  components: {
    Candidate, 
    Result
  },
  data () {
    return {
      e6: 1,
    }
  },
  
}
        
</script>