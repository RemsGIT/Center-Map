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
                <nav class="modal-menu">
                    <ul :class="`modal-menu-list ${active}`">
                        <li class="general" @click="switchMenu('general')" >Informations générales</li>
                        <li class="rooms" @click="switchMenu('rooms')">Salles</li>
                        <li class="amphi" @click="switchMenu('amphi')">Amphithéatres</li>
                    </ul>
                </nav>

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
export default {
    name: "Pop-up",
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
        }
    }
}
</script>

<style src="./popup.css"></style>
