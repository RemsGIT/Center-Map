<template>
    <div class="modal-overlay" @click="closeModal">
        <div class="modal" @click.prevent.stop>

            <div class="modal-close" @click="closeModal">
                <span>X</span>
            </div>
            <!-- Top image with close button -->
            <div class="modal-header">
                <img v-if="point.image !== ''" :src="`images/${point.image}.png`" alt="" style="width: 100%;max-height: 200px">
                <img v-else src="images/default.png" alt="" style="width: 100%;max-height: 200px">
            </div>

            <!-- Modal's content -->
            <div class="modal-content">
                <!-- Title -->
                <h1>{{ point.name }}</h1>

                <!-- Menu -->
                <Menu :list-menus="getMenuItems()" :point="point" @changeMenu="getNewMenu"/>

                <!-- Content -->
                <div class="modal-content" style="margin-top: 0;">
                    <UpjvContent :active="active" :point="point" v-if="point.type === 'upjvBuilding'"/>
                    <BuContent :active="active" :point="point" v-if="point.type === 'upjvBU'" />
                    <RuContent :active="active" :point="point" v-if="point.type === 'upjvRU'" />
                    <CrousContent :active="active" :point="point" v-if="point.type === 'crous'" />
                </div>


                <!-- Footer -->

                <div class="border"></div>
                <div class="modal-actions">
                    <div @click="showStreetView = true" class="btn">
                        <div class="streetViewIcon"></div>
                    </div>
                    <button class="button" @click="closeModal">Fermer</button>
                </div>
            </div>

            <street-view v-if="showStreetView" :url="point.gStreetViewLink" @stateModalStreetView="handleModalStreetView" />
        </div>
    </div>
</template>

<script>
import Menu from "@/components/Popup/Menu";
import UpjvContent from "@/components/Popup/Contents/UpjvContent";
import BuContent from "@/components/Popup/Contents/BuContent";
import RuContent from "@/components/Popup/Contents/RuContent";
import GoogleStreetView from "@/components/GoogleStreetView/GoogleStreetView";
import CrousContent from "@/components/Popup/Contents/CrousContent.vue";

export default {
    name: "Pop-up",
    components: {
        CrousContent,
        Menu,
        UpjvContent,
        BuContent,
        RuContent,
        'street-view': GoogleStreetView
    },
    props: {
        point: {
            type: Object,
            required: true,
            default: () => {}
        }
    },
    data() {
        return {
            active: "general",
            showStreetView: false
        }
    },
    methods: {
        getNewMenu(value){
            this.active = value
        },
        closeModal() {
            this.$emit('stateModal', 'close')
        },
        handleModalStreetView(value){
            // Change l'état de la modal : ouvre ou ferme
            switch (value){
                case 'open':
                    this.showStreetView = true
                    break;
                case 'close':
                    this.showStreetView = false;
                    break;
            }
        },
        getMenuItems(){
            switch(this.point.type){
                case 'upjvBuilding':
                    return {
                        general: 'Informations générales',
                        rooms: 'Salles',
                        amphi: 'Amphithéatres'
                    }
                case 'upjvBU':
                    return {
                        general: 'Informations générales',
                        subjects: 'Matières',
                        pictures: 'Photos'
                    }
                case 'upjvRU':
                    return {
                        general: 'Informations générales',
                        cafetaria: 'Cafétaria',
                        pictures: 'Photos'
                    }
            }
        }
    }
}
</script>

<style src="./popup.css"></style>
