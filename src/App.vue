<template>
  <v-app>
    <v-toolbar app>
      <v-btn icon>
        <v-img
        :src="require('./assets/kt_logo.png')"
        contain
        height="20"></v-img>
      </v-btn>
        <v-text-field
          v-model="keyword"
          append-outer-icon="search"
          @click:append-outer="search"
          clearable
        ></v-text-field>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-content>
      <Step/>
    </v-content>
  </v-app>
</template>

<script>
import Step from './components/Step'

export default {
  name: 'App',
  components: {
    Step
  },
  data () {
    return {
      keyword:''
    }
  },
  methods: {
    sendMessage () {
      this.clearKeyword()
    },
    clearKeyword () {
      this.keyword = ''
    },
    search () {
      console.log('search' + this.keyword)
      const baseURI = 'http://169.56.70.69:32578';
      this.$http.get(`${baseURI}/search?keyword=`+this.keyword)
      .then((result) => {
        console.log(result)
      })

    }
  }
}
</script>
