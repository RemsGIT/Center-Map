<template>
    <!-- Menu -->
    <nav class="modal-menu">
        <ul :class="`modal-menu-list ${active}`">
            <li v-for="(menu, key) in listMenus" :key="key" :class="key" @click="switchMenu(key)">
                {{menu}}
            </li>
        </ul>
    </nav>
</template>

<script>
export default {
    name: "menu-list",
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
            this.$emit('changeMenu', item)
        }
    }
}
</script>

<style scoped>

</style>
