<template>
  <v-container
   fluid 
   grid-list-md >
    <v-layout row>
        <v-flex xs12 md8>
            <div id="map" style="height:500px;width:100%"></div>
        </v-flex>
        <v-flex xs12 md4>
            <v-list two-line 
            class="scroll-y" 
            style="max-height: 500px">
                <v-subheader>pois</v-subheader>
                <template v-for="(item, i) in result.poi">
                    <!-- {{drawPoint(item.name+i, item.name, item.lat, item.lng)}} -->
                    <v-list-tile
                        :key="item.name + '-lat' + i"
                    >
                        <v-list-tile-content>
                            <v-list-tile-title v-html="item.name"></v-list-tile-title>
                            <v-list-tile-sub-title v-html="item.addressCode"></v-list-tile-sub-title>
                        </v-list-tile-content>
                    </v-list-tile>
                </template>
                <v-subheader>address</v-subheader>
                <template v-for="(item, i) in result.address">
                    <v-list-tile
                        :key="item.lat + '-lng' + i"
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
    props: ['result'],
    data: () => ({
        map: null,
        markerList: []
    }),
    mounted (){
        console.log('map')
        this.map=new window.olleh.maps.Map(document.getElementById('map'),{
            center: new window.olleh.maps.LatLng(37.57201137787062, 126.97888043751267),
            zoom: 8,
            panControl: false,
            mapTypeControl:false
        });
        this.eraseOnMap(this.markerList)
        this.drawAllMarkers(this.result.poi)
    },
    updated (){
        console.log('updated')
        this.eraseOnMap(this.markerList)
        this.drawAllMarkers(this.result.poi)
    },
    methods:{
        drawAllMarkers(pois){
            console.log('draw pois')
            console.log(pois)
            var lats = []
            var lngs = []
            for(var i=0, poi; poi=pois[i]; i++){
                console.log(poi.name)
                var icon = new window.olleh.maps.overlay.Marker({
                    id: poi.name,
                    position: new window.olleh.maps.LatLng(poi.lat, poi.lng),
                    map: this.map,
                    title: poi.name
                });
                lats.push(poi.lat)
                lngs.push(poi.lng)
                this.markerList.push(icon)
            }
            this.fitMap(lats, lngs)
        },
        findMaxMinValue(values){
            var result = []
            var lowest = values[0];
            var highest = values[0];
            for(var i=0, item; item=values[i]; i++){
                if(item < lowest){
                    lowest = item
                }else if(item > highest){
                    highest = item;
                }
            }
            result.push(lowest);
            result.push(highest);
            return result;
        },
        fitMap(lats, lngs){
            if(lats.length != 0 && lngs.length !=0){
                var fitLat = this.findMaxMinValue(lats);
                var fitLng = this.findMaxMinValue(lngs);
                var lb = new window.olleh.maps.LatLng(fitLat[0], fitLng[0]); // 좌측 하단 좌표
                var rt = new window.olleh.maps.LatLng(fitLat[1], fitLng[1]); // 우측 상단 좌표
                var bounds = new window.olleh.maps.Bounds(lb, rt);
                this.map.fitBounds(bounds);
            }
        },
        eraseOnMap(items){
            for(var i=0, item; item=items[i]; i++){
                item.erase();
                item.setMap(null);
            };
        }
        
    }
  }
</script>

