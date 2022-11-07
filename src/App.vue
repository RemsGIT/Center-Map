<template>
    <map-item @clickOnMarker="getMarkerClick"/>

    <transition name="fade" appear>
        <pop-up :point="currentPoint" v-if="showPopUp" @stateModal="changeStateModal"/>
    </transition>

</template>

<script>
import MapItem from "@/components/Map/MapItem";
import Popup from "@/components/Popup/Popup";

export default {
    name: 'App',
    components: {
        'map-item': MapItem,
        'pop-up': Popup
    },
    data() {
        return {
            showPopUp: false,
            currentPoint: {}
        }
    },
    methods: {
        getMarkerClick(point){
            this.changeStateModal('open')
            this.currentPoint = point
        },
        changeStateModal(value){
            // Change l'état de la modal : ouvre ou ferme
            switch (value){
                case 'open':
                    this.showPopUp = true
                    break;
                case 'close':
                    this.showPopUp = false;
                    break;
            }
        }
    }
}
</script>

<style>
@font-face {
    font-family: "Montserrat";
    src: url('./assets/fonts/Montserrat/Montserrat-Regular.ttf') format('truetype');
}
html, body {
    width: 100%;
    height: 100%;
    margin: 0
}

#app {
    position: relative;
    width: 100%;
    height: 100%;
    font-family: "Montserrat" ,serif;
}

</style>
