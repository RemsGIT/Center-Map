<template>
    <div class="modal-overlay" @click="closeModal">
        <div class="modal" @click.prevent.stop>

            <div class="modal-close" @click="closeModal">
                <span>X</span>
            </div>
            <!-- Top image with close button -->
            <div class="modal-header">
                <img src="https://dummyimage.com/450x175/000/fff" alt="">
            </div>

            <!-- Modal's content -->
            <div class="modal-content">
                <!-- Title -->
                <h1>{{ point.name }}</h1>

                <!-- Menu -->
                <Menu :list-menus="getMenuItems()" :point="point"/>

                <!-- Content of menu -->
                <div class="modal-content">
                    <!-- Informations générales -->
                    <template v-if="active === 'general'">
                    </template>

                    <!-- Les salles -->
                    <template v-if="active === 'rooms'">
                        {{point.rooms}}
                    </template>

                    <!-- Les amphithéatres -->
                    <template v-if="active === 'amphi'">
                        {{point.amphitheaters}}
                    </template>
                </div>

                <!-- Footer -->

                <div class="border"></div>
                <button class="button" @click="closeModal">Fermer</button>
            </div>
        </div>
    </div>
</template>

<script>
import Menu from "@/components/Popup/Menu";
export default {
    name: "Pop-up",
    components: {
        Menu
    },
    props: {
        point: {
            type: Object,
            required: true,
            default: () => {
            }
        }
    },
    data() {
        return {
            active: "general"
        }
    },
    methods: {
        switchMenu(item) {
            this.active = item
        },
        closeModal() {
            this.$emit('stateModal', 'close')
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
            }
        }
    }
}
</script>

<style src="./popup.css"></style>
