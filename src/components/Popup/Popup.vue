<template>
    <div class="modal-overlay" @click="closeModal">
            <div class="modal" @click.prevent.stop>
                <h1>{{ point.name }}</h1>
                <p>description</p>

                <button class="button" @click="closeModal">Fermer</button>
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
            default: () => {}
        }
    },
    methods: {
        closeModal(){
            this.$emit('stateModal', 'close')
        }
    }
}
</script>

<style src="./popup.css"></style>
