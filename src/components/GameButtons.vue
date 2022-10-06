<template>
    <div>
        <button class="prev" :style="showPrev ? '' : 'background: transparent; border: 0; color: transparent;'" type="button" @click="$emit('clickedPrev', true)">Prev</button>
        <button class="next" :style="showNext ? '' : 'background: transparent; border: 0; color: transparent;'" type="button" @click="$emit('clickedNext', true)">Next</button>
        <button class="btn-reset" type="button" @click="reset">Reset score board</button>
    </div>
</template>

<script>
    export default {
        name: 'GameButtons',
        emits: {
            clickedPrev: null,
            clickedNext: null
        },
        props: {
            showPrev: Boolean,
            showNext: Boolean
        },
        methods: {
            reset() {
                sessionStorage.clear()
                location.reload()
            }
        },
    }
</script>

<style scoped>
    button {
        min-height: 10vh;
        width: 100%;
    }
</style>