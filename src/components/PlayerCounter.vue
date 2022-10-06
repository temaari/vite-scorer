<template>
    <div class="player">
        <label for="playerCount">Number of players</label>
        <select name="player-count" id="player-count" :value="count"
            @change="addCount($event.target.value)"
        >
            <option :value="2">2</option>
            <option :value="3">3</option>
            <option :value="4">4</option>
            <option :value="5">5</option>
            <option :value="6">6</option>
            <option :value="7">7</option>
            <option :value="8">8</option>
            <option :value="9">9</option>
            <option :value="10">10</option>
        </select>
    </div>
</template>

<script>
    export default {
        name: 'PlayerCounter',
        methods: {
            addCount(value) {
                sessionStorage.setItem('player-count', Number(value))
            }
        },
        computed: {
            count() {
                if (sessionStorage.getItem('player-count') === null) return 2
                return Number(sessionStorage.getItem('player-count'))
            }
        }
    }
</script>

<style scoped>
    label {
        width: 100%;
        height: 10vh;
        font-size: 3ch;
    }
    #player-count {
        width: 100%;
        height: 10vh;
        font-size: 3ch;
        padding: 1rem;
        border-bottom: 1px solid black;
    }
</style>