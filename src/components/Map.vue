<template>
    <div class="container">
        <div id="map" class="map" ref="map"></div>
      <!--  <canvas id="deck-canvas" class="deck-canvas" ref="deck-canvas"></canvas>-->
        <Layers :viewState = 'viewState' :map="this.map"/>

    </div>
</template>

<script>
  /*  import {Deck} from '@deck.gl/core'
    import {ScatterplotLayer} from '@deck.gl/layers';*/
    import mapbox from 'mapbox-gl';
    /*import MglMap from 'vue-mapbox';*/
    import {MapboxLayer} from '@deck.gl/mapbox';
  /*  const earthquakes = require("../assets/earthquake-data.json");*/
    import Layers from "./Layers";






    export default {
        components: {
          /*  MglMap,*/
            Layers
        },
        data(){
            return {
                viewState: {
                    /*passing token is insecure, but it is public one and passed for simple test assignment check*/
                    accessToken: "pk.eyJ1Ijoia2FwYzNkIiwiYSI6ImNpbGpodG82czAwMmlubmtxamdsOHF0a3AifQ.xCbMUsy_a_0A9cd4GvjXKQ",
                    mapStyle: 'mapbox://styles/mapbox/light-v9',
                    /*mapData: earthquakes,*/
                    latitude: 21.521757,
                    longitude: -77.781167,
                    zoom: 1,
                    bearing: 0,
                    pitch: 0,
                    radius: 300
                },
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

           /* this.deck = new Deck({
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

            });*/
        },

    }
</script>

<style>
    .container {
        padding: 0;
        margin: 0;
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
/*    .deck-canvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }*/
</style>