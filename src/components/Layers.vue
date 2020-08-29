<template>
    <div>
        <canvas id="deck-canvas" class="deck-canvas" ref="deck-canvas"></canvas>
        <LayerSwitcherModule @choseLayer="choseLayer"/>
    </div>
</template>

<script>
    import {Deck} from '@deck.gl/core'
    import {ScatterplotLayer} from '@deck.gl/layers';
    import * as d3 from 'd3';
    import LayerSwitcherModule from "./LayerSwitcherModule";
    const earthquakes = require("../assets/earthquake-data.json");

    export default {
        name: "Earth-quake_layer",
        components: {
            LayerSwitcherModule
        },
        props: ['viewState'],
        data(){
            return {
                LAhouses: {},
                ukCitizens: {},
                itemId: ''
            }
        },
        created() {
            this.deck = null;
        },
        methods:{
            choseLayer(event){
                this.itemId = event.currentTarget.id;
                event.currentTarget.classList.add('red');
                let links = document.querySelectorAll('.layers-menu__item');
                for (let i = 0; i< links.length; i++){
                    if(links[i] === event.currentTarget) continue;
                    links[i].classList.remove('red');
                }

                if(this.itemId === 'earthquake-layer'){

                    this.deck.setProps({
                        layers: [
                            new ScatterplotLayer({
                                id: 'earthquake-layer',
                                data: earthquakes,
                                visible: true,
                                radiusScale: 10,
                                radiusMinPixels: 0.5,
                                getPosition: d => [Number(d.Longitude), Number(d.Latitude), 0],
                                getFillColor: [255, 0, 128],
                                getRadius: 100

                            })
                        ]
                    })
                } if (this.itemId === 'la-houses-layer'){
                    this.deck.setProps({
                        layers: [
                            new ScatterplotLayer({
                                id: 'la-houses-layer',
                                data: this.LAhouses,
                                visible: true,
                                radiusScale: 10,
                                radiusMinPixels: 0.5,
                                getPosition: d => [Number(d.center_lon), Number(d.center_lat), 0],
                                getFillColor: [128, 255, 0],
                                getRadius: 100
                            })
                        ]
                    })
                } if (this.itemId === 'uk-residents-layer'){
                    this.deck.setProps({
                        layers: [
                            new ScatterplotLayer({
                                id: 'uk-residents-layer',
                                data: this.ukCitizens,
                                visible: true,
                                radiusScale: 10,
                                radiusMinPixels: 0.5,
                                getPosition: d => [Number(d.workplace_lng), Number(d.workplace_lat), 0],
                                getFillColor: [102, 205, 170],
                                getRadius: 500
                            })
                        ]
                    })
                }

                },

            async fetchData(){
               let LaData = d3.csv("https://raw.githubusercontent.com/uber-web/kepler.gl-data/master/la_assessorparcels/data.csv").then(function (data) {
                    return data
                });
               let ukData = d3.csv("https://raw.githubusercontent.com/uber-web/kepler.gl-data/master/ukcommute/data.csv").then(function (data) {
                   return data
               });
               this.ukCitizens = ukData;
                this.LAhouses = LaData;

            }

        },
        mounted() {
            this.fetchData();
            this.deck = new Deck({
                canvas: 'deck-canvas',
                width: '100%',
                height: '100%',
                initialViewState: this.viewState,
                controller: true,
                onViewStateChange: ({viewState}) => {
                    this.$parent.map.jumpTo({
                        center: [viewState.longitude, viewState.latitude],
                        zoom: viewState.zoom,
                        bearing: viewState.bearing,
                        pitch: viewState.pitch
                    });
                },

                layers: [

                ]

            });
        }
    }
</script>

<style scoped>
    .deck-canvas {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
</style>