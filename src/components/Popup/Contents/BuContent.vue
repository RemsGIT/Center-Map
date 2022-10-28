<template>
    <div>
        <!-- Informations générales -->
        <template v-if="active === 'general'">
            info générales de la bu
        </template>

        <!-- Les salles -->
        <template v-if="active === 'subjects'">
            {{point.subjects}}
        </template>

        <!-- Les amphithéatres -->
        <template v-if="active === 'pictures'">
            les photos
            {{point.pictures}}
        </template>
    </div>
</template>

<script>
export default {
    name: "BuContent",
    props: ['active', 'point']
}
</script>

<style scoped>

</style>
