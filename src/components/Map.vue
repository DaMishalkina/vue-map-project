<template>
    <div class="container">
       <!-- <MglMap
        :access-token="accessToken"
        :map-style="mapStyle"
        :center="[longitude, latitude]"
        :zoom = "zoom"
        :bearing="bearing"
        :pitch="pitch"
        @load="loadLayers"
        />
        <canvas id="app"></canvas>-->
        <div id="map" class="map" ref="map"></div>
        <canvas id="deck-canvas" class="deck-canvas" ref="deck-canvas"></canvas>
    </div>
</template>

<script>
    import {Deck} from '@deck.gl/core'
    import {ScatterplotLayer} from '@deck.gl/layers';
    import mapbox from 'mapbox-gl';
    import MglMap from 'vue-mapbox';
    import {MapboxLayer} from '@deck.gl/mapbox';
    const earthquakes = require("../assets/earthquake-data.json");





    export default {
        components: {
            MglMap
        },
        data(){
            return {
                viewState: {
                    /*passing token is insecure, but it is public one and passed for simple test assignment check*/
                    accessToken: "pk.eyJ1Ijoia2FwYzNkIiwiYSI6ImNpbGpodG82czAwMmlubmtxamdsOHF0a3AifQ.xCbMUsy_a_0A9cd4GvjXKQ",
                    mapStyle: 'mapbox://styles/mapbox/light-v9',
                    mapData: earthquakes,
                    latitude: 36.08,
                    longitude: -121.07083,
                    zoom: 5,
                    bearing: 0,
                    pitch: 0,
                    radius: 300
                }
            };
        },

        created() {
            this.map = null;
            this.deck = null;
        },

        mounted() {
            this.map = new mapbox.Map({
                accessToken: this.viewState.accessToken,
                container: 'map',
                interactive: true,
                style: this.viewState.mapStyle,
                center: [this.viewState.longitude, this.viewState.latitude],
                zoom: this.viewState.zoom,
                pitch: this.viewState.pitch,
                bearing: this.viewState.bearing,
            });

            this.deck = new Deck({
                canvas: 'deck-canvas',
                width: '100%',
                height: '100%',
                initialViewState: this.viewState,
                controller: true,
                onViewStateChange: ({viewState}) => {
                    this.map.jumpTo({
                        center: [viewState.longitude, viewState.latitude],
                        zoom: viewState.zoom,
                        bearing: viewState.bearing,
                        pitch: viewState.pitch
                    });
                },

                layers: [
                    new ScatterplotLayer({
                        id: 'scatter-plot',
                        data: this.viewState.mapData,
                        radiusScale: 10,
                        radiusMinPixels: 0.5,
                        getPosition: d => [Number(d.Longitude), Number(d.Latitude), 0],
                        getFillColor: [255, 0, 128],
                        getRadius: 100

                    })
                ]

            });
        },

   /*     computed: {
            getLayers(){
               const earthquakeLayer = new ScatterplotLayer({
                   id: 'scatter-plot',
                   // data: this.viewState.mapData,
                   data: [{position: [-121.50217, 37.0705, 0]}],
                  /!* radiusScale: this.viewState.radius,
                   radiusMinPixels: 400,*!/
                   /!*getPosition: d => [Number(d.lng), Number(d.lat)],*!/
                   getFillColor: [255, 0, 128],
                   getRadius: 10000
               });
               console.log(1)
               return [earthquakeLayer]
            }
        },

        methods: {
            renderLayers(layers){
                this.deck.setProps({
                    layers
                })
            }
        },

        watch: {
            getLayers(layers){
                this.renderLayers(layers);
            }
        }*/

    }
</script>

<style>
    .container {
        width: 100%;
        height: 100vh;
        position: relative;
    }
    .map {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow: hidden;

    }
    .deck-canvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
</style>