<template>
    <p>
        <button v-if="showPrev" type="button" @click="$emit('clickedPrev', true)">Prev</button>
        <button v-else type="button" style="background: transparent; border: 0;;" disabled></button>
        <button v-if="showNext" type="button" @click="$emit('clickedNext', true)">Next</button>
        <button class="reset" type="button" @click="reset">Reset score board</button>
    </p>
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
    p {
        margin-top: 0vh;
        width: 100%;
        font-size: 3ch;
    }
    button {
        width: 49%;
        border-radius: 10px;
        background: grey;
        height: 10vh;
    }
    p > :first-child {
        margin-right: 2%;
    }
    .reset {
        margin-top: 1rem;
        width: 100%;
    }
</style>