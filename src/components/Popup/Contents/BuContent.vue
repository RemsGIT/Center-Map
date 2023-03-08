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
                <span v-if="point.hours" v-html="point.hours"></span>
                <p class="content-group-text" v-else>
                    Les horaires ne sont pas renseignées.
                </p>
            </div>

            <!-- Accessibilité -->
            <div class="content-group">
                <i class="fa-solid fa-car"></i> Accessibilité
                <hr>
                <template v-if="point.access">{{point.access}}</template>
                <p class="content-group-text" v-else>
                    Aucune information sur l'accessibilité du lieu n'est renseignée.
                </p>
            </div>

        </template>

        <!-- Les salles -->
        <template v-if="active === 'subjects'">
            <ul>
                <li v-for="(element, key) in getSubjects(point.subjects)" :key="key">
                    {{getName(element)}}
                </li>
            </ul>
        </template>

        <!-- Les amphithéatres -->
        <template v-if="active === 'pictures'">
            <p class="content-group-text">
                Aucune photo n'est renseignée.
            </p>
        </template>
    </div>
</template>

<script>
export default {
    name: "BuContent",
    props: ['active', 'point'],
    methods: {
        getSubjects(value) {
            return value.replace(/\[|\]/g,'').split(',')
        },
        getName(value){
            return value.substring(1, value.length - 1)
        },
    }
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
