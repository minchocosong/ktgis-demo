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
          @keyup.enter="search"
          clearable
        ></v-text-field>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-content>
      <v-progress-linear v-if="progressing" :indeterminate="true"></v-progress-linear>
      <Step v-if="searchResult !== ''" :result="searchResult" :keyword="keyword"/>
       <v-carousel height="800" v-if="searchResult == ''" >
          <v-carousel-item
            v-for="(item,i) in items"
            :key="i"
            :src="item.src"
          ></v-carousel-item>
        </v-carousel>
    </v-content>
  </v-app>
</template>

<script>
import Step from './components/Step'
import sample from './sample.json'

export default {
  name: 'App',
  components: {
    Step
  },
  data () {
    return {
      keyword:'',
      searchResult: '',
      progressing: false,
        items: [
          {
            src: require('./assets/talk.jpeg')
          },
          {
            src: require('./assets/develop.jpeg')
          }
        ]
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
      this.progressing = true
      const baseURI = 'http://169.56.70.69:32578';
      this.$http.get(`${baseURI}/search?test=true&keyword=`+this.keyword)
      .then((result) => {
        this.progressing = false
        console.log(result)
        if(result !== null && result.data !== null && result.data.data !== null){
          this.searchResult = result.data.data
        }else{
          console.log('data has error')
        }
      }).catch(error => {
          this.progressing = false
          console.log(error)
      });

    }
  }
}
</script>
