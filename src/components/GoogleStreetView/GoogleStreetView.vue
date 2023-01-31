<template>
    <div class="modal-overlay" @click="closeModal">
        <div class="modal modal-lg" @click.prevent.stop>

            <div class="modal-close" @click="closeModal">
                <span>X</span>
            </div>
           
            <!-- Modal's content -->
            <div class="modal-content">
                <iframe :src="url" width="800" height="500" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "GoogleStreetView",
    props: {
        url: {
            type: String,
            required: true,
        }
    },
    methods: {
        closeModal(){
            this.$emit('stateModalStreetView', 'close')
        }
    }
}
</script>

<style src="./googlestreetview.css"></style>