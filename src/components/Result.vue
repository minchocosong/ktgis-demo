<template>
  <v-container fluid grid-list-md >
    <v-layout row wrap>
        <v-flex xs12 md8>
            <div id="map" style="height:500px;width:100%"></div>
        </v-flex>
        <v-flex xs12 md4>
            <v-list two-line>
                <v-subheader>pois</v-subheader>
                <template v-for="(item) in result.poi">
                    <v-list-tile
                        :key="item.name"
                    >
                        <v-list-tile-content>
                        <v-list-tile-title v-html="item.name"></v-list-tile-title>
                        <v-list-tile-sub-title v-html="item.addressCode"></v-list-tile-sub-title>
                        </v-list-tile-content>
                    </v-list-tile>
                </template>
                <v-subheader>address</v-subheader>
                <template v-for="(item) in result.address">
                    <v-list-tile
                        :key="item.name"
                    >
                        <v-list-tile-content>
                        <v-list-tile-title>{{item.siDo + ' ' + item.siGunGu + ' ' + item.dong + ' (' + item.street +')'}}</v-list-tile-title>
                        </v-list-tile-content>
                    </v-list-tile>
                </template>
            </v-list>       
        </v-flex>
        
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: 'Result',
    data: () => ({
      open: ['poi'],
      tree: [],
      result: {
        poi: [
            {
                name: "남산타워",
                addressCode: "1100000000",
                lat: 37.123125325,
                lng: 127.13324234
            },
            {
                name: "남산타워 주차장",
                addressCode: "1100000000",
                lat: 37.123125325,
                lng: 127.13324234
            }
        ],
        address: [
            {
                siDo: "서울특별시",
                siGunGu: "용산구",
                dong: "용산동2가",
                street: "남산공원길",
                lat: 37.123125325,
                lng: 127.13324234
            }
        ]
      }
    }),
    mounted (){
        new window.olleh.maps.Map(document.getElementById('map'),{
            center: new window.olleh.maps.LatLng(37.57201137787062, 126.97888043751267),
            zoom: 8,
            panControl: false,
            mapTypeControl:false
        });
    }
  }
</script>
