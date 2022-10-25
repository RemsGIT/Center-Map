<template>
    <map-item/>
</template>

<script>
import MapItem from "@/components/Map/MapItem";

export default {
    name: 'App',
    components: {
        'map-item': MapItem
    }
}
</script>

<style>
html, body {
    width: 100%;
    height: 100%;
    margin: 0
}

#app {
    width: 100%;
    height: 100%;
}
</style>
