<template>
    <div id="app-map" ></div>
</template>

<script>
import Leaflet from 'leaflet'
import upjvPoints from "../../../data/points/upjv";
import buPoints from "../../../data/points/bibliotheque";
import geojson from "../../../data/geojson/geojson";

export default {
    name: "MapItem",
    data() {
        return {
            upjvPoints: upjvPoints,
            buPoints: buPoints,
            map: null,
        }
    },
    mounted() {
        let map;
        
        // Geojson
        const geoJson =  Leaflet.geoJSON(geojson, {
            onEachFeature: (feature,layer) => {
                layer.setStyle({
                    color: 'blue',
                    colorFill: 'blue'
                })

                layer.on('click', () => this.clickOnPolygon(layer))

                layer.on('mouseover', () => {
                    layer.setStyle({
                        color: 'red',
                        colorFill: 'red'
                    })
                })
                layer.on('mouseout', () => {
                    layer.setStyle({
                        color: 'blue',
                        colorFill: 'blue'
                    })
                })
            }
        });
        const geoJsonBU = Leaflet.geoJSON(geojson, {
            filter: (feature) => {
                return feature.properties.type === "upjvBU"
            },
            onEachFeature: (feature,layer) => {
                layer.setStyle({
                    color: 'blue',
                    colorFill: 'blue'
                })

                layer.on('click', () => this.clickOnPolygon(layer))

                layer.on('mouseover', () => {
                    layer.setStyle({
                        color: 'red',
                        colorFill: 'red'
                    })
                })
                layer.on('mouseout', () => {
                    layer.setStyle({
                        color: 'blue',
                        colorFill: 'blue'
                    })
                })
            }
        })
        const geoJsonUPJV = Leaflet.geoJSON(geojson, {
            filter: (feature) => {
                return feature.properties.type === "upjvBuilding"
            },
            onEachFeature: (feature,layer) => {
                layer.setStyle({
                    color: 'purple',
                    colorFill: 'purple'
                })

                layer.on('click', () => this.clickOnPolygon(layer))

                layer.on('mouseover', () => {
                    layer.setStyle({
                        color: 'red',
                        colorFill: 'red'
                    })
                })
                layer.on('mouseout', () => {
                    layer.setStyle({
                        color: 'purple',
                        colorFill: 'purple'
                    })
                })
            }
        })
        const geoJsonRU = Leaflet.geoJSON(geojson, {
            filter: (feature) => {
                return feature.properties.type === "upjvRU"
            },
            onEachFeature: (feature,layer) => {
                layer.setStyle({
                    color: 'yellow',
                    colorFill: 'yellow'
                })

                layer.on('click', () => this.clickOnPolygon(layer))

                layer.on('mouseover', () => {
                    layer.setStyle({
                        color: 'red',
                        colorFill: 'red'
                    })
                })
                layer.on('mouseout', () => {
                    layer.setStyle({
                        color: 'yellow',
                        colorFill: 'yellow'
                    })
                })
            }
        })
        
        const layers = {
            'BU': geoJsonBU,
            'UPJV': geoJsonUPJV,
            'RU': geoJsonRU
        };
        
        const layers2 = [geoJsonBU, geoJsonUPJV, geoJsonRU]
        const options = {
            zoomControl: false,
            attributionControl: false,
            layers: layers2
        } 

        map = Leaflet.map('app-map', options).setView([0,0], 17)
            //.setView([49.89894695738625, 2.2990339994430546], 17);
        map.on('click', (e) => {
            console.log(e.latlng)
        })
        
        Leaflet.control.layers(null,layers).addTo(map)
        
        map.fitBounds(geoJson.getBounds())
        

        // Génération du fond de carte
        Leaflet.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}@2x?access_token=pk.eyJ1IjoicmVteWNhcyIsImEiOiJjbDlvOWs4Y3UwY2xsNDFrNGRqNDIxMThvIn0.052x69fiyb0ek6wqvOjGMA', {
            maxZoom: 19,
            id: 'mapbox/outdoors-v12',
            zoomOffset: -1,
            tileSize: 512,
            accessToken: "pk.eyJ1IjoicmVteWNhcyIsImEiOiJjbDlvOWs4Y3UwY2xsNDFrNGRqNDIxMThvIn0.052x69fiyb0ek6wqvOjGMA",
        }).addTo(map);
        
        this.map = map
    },
    methods: {
        clickOnPolygon(layer){
            console.log(layer)
            this.map.fitBounds(layer.getBounds())
            this.$emit('clickOnMarker', layer.feature.properties)
        },
    }
}
</script>

<style scoped src="./map.css">
.text-labels {
    font-size: 2em;
    font-weight: 700;
    color: white;
    /* Use color, background, set margins for offset, etc */
}
</style>

