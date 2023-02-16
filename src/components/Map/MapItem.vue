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
            controlLayers: null,
        }
    },
    mounted() {
        let map;
        
        // Geojson
        
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
        const geoJsonCROUS = Leaflet.geoJSON(geojson, {
            filter: (feature) => {
                return feature.properties.type === "crous"
            },
            onEachFeature: (feature,layer) => {
                layer.setStyle({
                    color: 'red',
                    colorFill: 'red'
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
                        color: 'red',
                        colorFill: 'red'
                    })
                })
            }
        })
        
        const layers = {
            'Bibliothèque universitaire': geoJsonBU,
            'Bâtiment UPJV': geoJsonUPJV,
            'Restaurant universitiare': geoJsonRU,
            'Crous': geoJsonCROUS
        };
        
        const layers2 = [geoJsonBU, geoJsonUPJV, geoJsonRU, geoJsonCROUS]
        const options = {
            zoomControl: false,
            attributionControl: false,
            layers: layers2,
        } 

        map = Leaflet.map('app-map', options).setView([49.89863424051644, 2.2990098595619206], 17)
            //.setView([49.89894695738625, 2.2990339994430546], 17);
        map.on('click', (e) => {
            console.log(e.latlng)
        })
        
        const controlLayer = Leaflet.control.layers(null,layers, {collapsed: false}).addTo(map)
        this.controlLayers = controlLayer
        this.resizeControlLayer(controlLayer)
        this.responsiveControlLayer(controlLayer)
        
        // Style the control
        document.querySelectorAll('.leaflet-control-container .leaflet-control-layers .leaflet-control-layers-overlays label').forEach(e => {
            e.style.padding = '8px 5px'
            e.style.cursor = 'pointer'
        })
        //map.fitBounds(geoJson.getBounds())
        

        // Génération du fond de carte
        Leaflet.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}@2x?access_token=pk.eyJ1IjoicmVteWNhcyIsImEiOiJjbDlvOWs4Y3UwY2xsNDFrNGRqNDIxMThvIn0.052x69fiyb0ek6wqvOjGMA', {
            maxZoom: 19,
            id: 'mapbox/outdoors-v12',
            zoomOffset: -1,
            tileSize: 512,
        }).addTo(map);
        
        this.map = map
    },
    methods: {
        clickOnPolygon(layer){
            this.map.fitBounds(layer.getBounds())
            this.$emit('clickOnMarker', layer.feature.properties)
        },
        responsiveControlLayer(controlButton){
            window.addEventListener("resize", () => this.resizeControlLayer(controlButton))
        },
        resizeControlLayer(controlButton){
            const width = window.innerWidth

            if(width <= 800) {
                controlButton.collapse();
                document.querySelector('.leaflet-control-container .leaflet-top.leaflet-right').style.top = '0'
                document.querySelector('.leaflet-control-layers').addEventListener('mouseleave', this.collapseControl);
                document.querySelector('.leaflet-control-layers-toggle').addEventListener('mouseenter', this.expandControl);
            }
            else {
                controlButton.expand();
                document.querySelector('.leaflet-control-container .leaflet-top.leaflet-right').style.top = '300px'
                document.querySelector('.leaflet-control-layers').removeEventListener('mouseleave', this.collapseControl);
                document.querySelector('.leaflet-control-layers-toggle').removeEventListener('mouseenter', this.expandControl);
            }
        },
        collapseControl(){
            this.controlLayers.collapse()
        },
        expandControl(){
            this.controlLayers.expand()
        }
    }
}
</script>

<style src="./map.css">
.text-labels {
    font-size: 2em;
    font-weight: 700;
    color: white;
    /* Use color, background, set margins for offset, etc */
}
</style>

