<template>
    <div class="container">
        <div id="map" class="map" ref="map"></div>
        <Layers :viewState = 'viewState' :map="this.map"/>

    </div>
</template>

<script>

    import mapbox from 'mapbox-gl';
    import Layers from "./Layers";






    export default {
        components: {
            Layers
        },
        data(){
            return {
                viewState: {
                    /*passing token is insecure, but it is public one and passed for simple test assignment check*/
                    accessToken: "pk.eyJ1Ijoia2FwYzNkIiwiYSI6ImNpbGpodG82czAwMmlubmtxamdsOHF0a3AifQ.xCbMUsy_a_0A9cd4GvjXKQ",
                    mapStyle: 'mapbox://styles/mapbox/light-v9',
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

</style>