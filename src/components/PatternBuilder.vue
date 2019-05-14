<template>
  <v-container fluid grid-list-md >
    <v-layout row wrap>
        <v-flex xs12 md8>
           <v-card>
                <v-card-title class="subheading font-weight-bold">Pattern Builder</v-card-title>
                <v-divider></v-divider>
                <v-card-text>
                    <v-list>
                         <v-list-tile>
                            <v-list-tile-content>Pattern : {{result.pattern}}</v-list-tile-content>
                         </v-list-tile>
                          <v-list-tile>
                            <v-list-tile-content>Original Keyword : {{result.originalKeyword}}</v-list-tile-content>
                         </v-list-tile>
                          <v-list-tile>
                            <v-list-tile-content>Refined Keyword : {{result.refinedKeyword}}</v-list-tile-content>
                         </v-list-tile>
                    </v-list>
                    
                </v-card-text>
           </v-card>
        </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: 'PatternBuilder',
    props: ['result'],
    data: () => ({
    }),
    mounted (){
        
    }
  }
</script>
