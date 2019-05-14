<template>
  <v-container fluid grid-list-md >
    <v-layout 
        row     
        wrap
        align-content-center
        justify-center
        >
        <v-flex
            xs12
            sm6
            md4
            >
            <v-card>
                <v-card-title class="subheading font-weight-bold">Address Service</v-card-title>
                <v-divider></v-divider>
                <v-data-iterator
                    :items= "steps.Address.candidateList"
                    hide-actions
                    class="token_list"
                    >
                    <template v-slot:item="props">
                        <div class="token_list">
                            <strong>TokenList</strong>
                            <v-data-iterator
                            :items= "props.item.tokenList"
                            hide-actions
                            content-tag="v-layout"
                            row
                            class="token_list"
                            >
                                <template v-slot:item="props">
                                    <v-flex xs12 sm6 md4 lg3>
                                        <v-text-field
                                        :value= "props.item.name"
                                        :hint= "props.item.type"
                                        persistent-hint
                                        solo
                                        readonly
                                        />
                                    </v-flex>
                                </template>
                            </v-data-iterator>
                            <!-- information --> 
                            <template v-if="props.item.address">
                                <strong>Information</strong><br>
                                <v-icon>place</v-icon>
                                <span>{{ props.item.address.code }} / {{ props.item.address.name }} </span>
                            </template>
                        </div>        
                    </template>
                </v-data-iterator>
            </v-card>
        </v-flex>
        <v-flex
            xs12
            sm6
            md4
            >
            <v-card>
                <v-card-title class="subheading font-weight-bold">Landmark Service</v-card-title>
                <v-divider></v-divider>
                <v-data-iterator
                    :items= "steps.Landmark.candidateList"
                    hide-actions
                    class="token_list"
                    >
                    <template v-slot:item="props">
                        <div class="token_list">
                            <strong>TokenList</strong>
                            <v-data-iterator
                            :items= "props.item.tokenList"
                            hide-actions
                            content-tag="v-layout"
                            row
                            class="token_list"
                            >
                                <template v-slot:item="props">
                                    <v-flex xs12 sm6 md4 lg3>
                                        <v-text-field
                                        :value= "props.item.name"
                                        :hint= "props.item.type"
                                        persistent-hint
                                        solo
                                        readonly
                                        />
                                    </v-flex>
                                </template>
                            </v-data-iterator>
                            <!-- information --> 
                            <template v-if="props.item.landmark">
                                <strong>Information</strong><br>
                                <v-icon>business</v-icon>
                                <span>{{ props.item.landmark.name }} </span>
                            </template>
                        </div>
                    </template>
                </v-data-iterator>
            </v-card>
        </v-flex>
        <v-flex
            xs12
            sm6
            md4
            >
            <v-card>
                <v-card-title class="subheading font-weight-bold">Dictionary Service</v-card-title>
                <v-divider></v-divider>
                <v-data-iterator
                    :items= "steps.Dictionary.candidateList"
                    hide-actions
                    class="token_list"
                    >
                    <template v-slot:item="props">
                        <div class="token_list">
                            <strong>TokenList</strong>
                            <v-data-iterator
                            :items= "props.item.tokenList"
                            hide-actions
                            content-tag="v-layout"
                            row
                            class="token_list"
                            >
                                <template v-slot:item="props">
                                    <v-flex xs12 sm6 md4 lg3>
                                        <v-text-field
                                        :value= "props.item.name"
                                        :hint= "props.item.type"
                                        persistent-hint
                                        solo
                                        readonly
                                        />
                                    </v-flex>
                                </template>
                            </v-data-iterator>
                        </div>
                    </template>
                </v-data-iterator>
            </v-card>
        </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: 'Candidate',
    props: ['steps'],
    data: () => ({
      styleObject: {
        padding: '5px'
      },
    })
  }
</script>
<style>
.token_list{
    padding: 5px
}
</style>
