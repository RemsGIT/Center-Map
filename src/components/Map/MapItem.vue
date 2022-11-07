<template>
    <div id="app-map" ></div>
</template>

<script>
import leaflet from 'leaflet'
import upjvPoints from "../../../data/points/upjv";
import buPoints from "../../../data/points/bibliotheque";
import geojson from "../../../data/geojson/geojson";

export default {
    name: "MapItem",
    data() {
        return {
            upjvPoints: upjvPoints,
            buPoints: buPoints
        }
    },
    mounted() {
        let map;

        map = leaflet.map('app-map').setView([49.89894695738625, 2.2990339994430546], 17);

        map.on('click', (e) => {
            console.log(e.latlng)
        })


        // Génération des markers bâtiment UPJV
        this.upjvPoints.forEach((element) => {
            new leaflet.Marker([element.lat, element.lng]).on('click', () => {this.clickOnMarker(element)}).addTo(map)
        })

        // Génération des markers bibliothèque universitaire
        this.buPoints.forEach((element) => {
            new leaflet.Marker([element.lat, element.lng]).on('click', () => {this.clickOnMarker(element)}).addTo(map)
        })

        // Chargement du geoJSON
        leaflet.geoJSON(geojson).addTo(map)

        // Génération du fond de carte
        leaflet.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoicmVteWNhcyIsImEiOiJjbDlvOWs4Y3UwY2xsNDFrNGRqNDIxMThvIn0.052x69fiyb0ek6wqvOjGMA', {
            maxZoom: 19,
            attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
            id: 'mapbox/streets-v11',
            zoomOffset: -1,
            tileSize: 512,
            accessToken: "pk.eyJ1IjoicmVteWNhcyIsImEiOiJjbDlvOWs4Y3UwY2xsNDFrNGRqNDIxMThvIn0.052x69fiyb0ek6wqvOjGMA"
        }).addTo(map);
    },
    methods: {
        clickOnMarker(point){
            this.$emit('clickOnMarker', point)
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

