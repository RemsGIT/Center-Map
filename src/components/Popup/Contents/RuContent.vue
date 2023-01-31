<template>
    <div>
        <!-- Informations générales -->
        <template v-if="active === 'general'">
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
                <i class="fa-brands fa-accessible-icon"></i> Accessibilité
                <hr>
                <template v-if="point.access">{{point.access}}</template>
                <p class="content-group-text" v-else>
                    Aucune information sur l'accessibilité du lieu n'est renseignée.
                </p>
            </div>

        </template>

        <!-- Les salles -->
        <template v-if="active === 'cafetaria'">
            cafet
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
    name: "RuContent",
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
    font-size: 12px;
}
</style>