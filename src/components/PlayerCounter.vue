<template>
    <div class="content-flex-box">
        <div class="content-flex-item">
            <div class="player-count">
                <label for="count-select">Number of players</label>
                <select class="count-select" name="count-select" id="count-select" :value="count"
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
        </div>
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
    .player-count {
        display: flex;
        flex-direction: column;
    }
    .count-select {
        background: lightgrey;
        border: 0;
        outline: 0;
        height: 5vh;
        font-size: 1ch;
        text-align: center;
    }
</style>