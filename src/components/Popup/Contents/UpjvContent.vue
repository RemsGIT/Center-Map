<template>
    <div>
        <!-- Informations générales -->
        <template v-if="active === 'general'">
            info générales du bâtiment upjv
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
</template>

<script>
export default {
    name: "UpjvContent",
    props: ['active', 'point']
}
</script>

<style scoped>

</style>
