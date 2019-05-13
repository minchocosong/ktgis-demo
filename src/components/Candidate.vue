<template>
  <v-container fluid grid-list-md >
    <v-data-iterator
    :items="candidateList"
    hide-actions
    content-tag="v-layout"
    row
    wrap
    align-content-center
    justify-center
    >
        <template v-slot:item="props">
            <v-flex
                xs12
                sm6
                md4
                >
                <v-card>
                    <v-card-title class="subheading font-weight-bold">{{ props.item.name }}</v-card-title>
                    <v-divider></v-divider>
                    <div class="token_list">
                        <!-- tokenList -->
                        <strong>TokenList</strong>
                        <v-data-iterator
                        :items= "props.item.tokenList"
                        hide-actions
                        content-tag="v-layout"
                        row
                        class="token_list"
                        >
                            <template v-slot:item="props">
                                <v-flex
                                xs12
                                sm6
                                md4
                                lg3
                                >
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
                        <strong v-if="props.item.name !== 'Dictionary Service'">Information</strong><br>
                        <v-icon v-if="props.item.name === 'Address Service'">place</v-icon>
                        <v-icon v-if="props.item.name === 'Landmark Service'">business</v-icon>
                        <span v-if="props.item.name === 'Address Service'">{{ props.item.information.code }} / {{ props.item.information.name }} </span>
                        <span v-if="props.item.name === 'Landmark Service'">{{ props.item.information.name }} </span>
                    </div>
                </v-card>
            </v-flex>
        </template>
    </v-data-iterator>
  </v-container>
</template>

<script>
  export default {
    name: 'Candidate',
    data: () => ({
      styleObject: {
        padding: '5px'
      },
      candidateList: [
        {
          name: 'Address Service',
          tokenList: [
            {
                name: "서울",
                type: "SIDO"
            },
            {
                name: "영등포구",
                type: "SIGUNGU"
            },
            {
                name: "여의도",
                type: "DONG"
            },
            {
                name: "ifc몰",
                type: ""
            },
            {
                name: "주차장",
                type: ""
            }
          ],
          information: {
            code: "1156011000",
            name: "여의도동"
          }
        },
        {
          name: 'Landmark Service',
          tokenList: [
            {
                name: "서울",
                type: ""
            },
            {
                name: "영등포구",
                type: ""
            },
            {
                name: "여의도ifc몰",
                type: "LANDMARK"
            },
            {
                name: "주차장",
                type: ""
            }
          ],
          information: {
            name: "남산타워",
            id: "0ffab65a-c58f-44c0-87dd-75c37f60ae57",
            categoryName: "명소",
            categoryCode: "11",
            addressCode: "1100000000",
            lat: 37.823637,
            lng: 127.196286
          }
        },
        {
          name: 'Dictionary Service',
          tokenList: [
            {
                name: "서울",
                type: ""
            },
            {
                name: "영등포구",
                type: ""
            },
            {
                name: "여의도",
                type: ""
            },
            {
                name: "ifc몰",
                type: ""
            },
            {
                name: "주차장",
                type: "CATEGORY"
            }
          ],
          information: {
            code: "110000",
          }
        }
      ]
    })
  }
</script>
<style>
.token_list{
    padding: 5px
}
</style>
