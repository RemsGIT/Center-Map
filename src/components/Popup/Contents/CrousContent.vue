<template>
    <div>
        <!-- Adresse -->
        <div class="content-group">
            <i class="fa-regular fa-map"></i> Adresse
            <hr>
            <template v-if="point.address">{{point.address}}</template>
            <p class="content-group-text" v-else>
                Aucune adresse n'est renseignée.
            </p>
        </div>

        <!-- Horaires -->
        <div class="content-group">
            <i class="fa-regular fa-clock"></i> Horaires
            <hr>
            <template v-if="point.hours">{{point.hours}}</template>
            <p class="content-group-text" v-else>
                Les horaires ne sont pas renseignées.
            </p>
        </div>

        <!-- Accessibilité -->
        <div class="content-group">
            <i class="fa-solid fa-car"></i> Accessibilité
            <hr>
            <template v-if="point.address">{{point.access}}</template>
            <p class="content-group-text" v-else>
                Aucune information sur l'accessibilité du lieu n'est renseignée.
            </p>
        </div>
    </div>

</template>


<script>
export default {
    name: "CrousContent",
    props: ['active', 'point']
}
</script>

<style scoped>
.content-group {
    display: block;
    margin-top: 30px;
}
.content-group-text{
    color: gray;
    font-size: 14px;
}
</style>
