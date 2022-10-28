<template>
    <!-- Menu -->
    <nav class="modal-menu">
        <ul :class="`modal-menu-list ${active}`">
            <li v-for="(menu, key) in listMenus" :key="key" :class="key" @click="switchMenu(key)">
                {{menu}}
            </li>
        </ul>
    </nav>

    <div class="modal-content">
        <UpjvContent :active="active" :point="point" v-if="point.type === 'upjvBuilding'"/>
        <BuContent :active="active" :point="point" v-if="point.type === 'upjvBU'" />
    </div>
</template>

<script>
import UpjvContent from "@/components/Popup/Contents/UpjvContent";
import BuContent from "@/components/Popup/Contents/BuContent";
export default {
    name: "menu-list",
    components: {
        UpjvContent,
        BuContent,
    },
    props: {
        listMenus: {
            type: Object,
            default: () => {}
        },
        point: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            active: "general"
        }
    },
    methods: {
        switchMenu(item) {
            this.active = item
        }
    }
}
</script>

<style scoped>

</style>
