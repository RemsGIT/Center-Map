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
                <i class="fa-solid fa-car"></i> Accessibilité
                <hr>
                <template v-if="point.address">{{point.access}}</template>
                <p class="content-group-text" v-else>
                    Aucune information sur l'accessibilité du lieu n'est renseignée.
                </p>
            </div>
        </template>

        <!-- Les salles -->
        <template v-if="active === 'rooms'">
            <template v-if="point.rooms.length > 2">
                <ul>
                    <li v-for="(room, key) in getRooms(point.rooms)" :key="key">
                        {{getName(room)}}
                    </li>
                </ul>
            </template>
            <p v-else class="content-group-text">Aucune salle n'est renseignée pour ce bâtiment.</p>
        </template>

        <!-- Les amphithéatres -->
        <template v-if="active === 'amphi'">
            <p v-if="point.amphitheaters.length <= 2" class="content-group-text">Il n'y a pas d'amphithéatre dans ce bâtiment.</p>
            <template v-else>
                <ul>
                    <li v-for="(amphi, key) in JSON.parse(point.amphitheaters)" :key="key">
                        <b>{{amphi.name}}</b> : {{amphi.seats}} places
                    </li>
                </ul>
            </template>
        </template>
    </div>
</template>

<script>
export default {
    name: "UpjvContent",
    props: ['active', 'point'],
    methods: {
        getName(value){
            return value.substring(1, value.length - 1)
        },
        getRooms(value) {
            return value.replace(/\[|\]/g,'').split(',')
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
    font-size: 14px;
}
</style>

