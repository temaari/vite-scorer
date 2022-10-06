<template>
    <div>
        <label class="game-title">Enter names</label>
        <span v-for="i in count" :key="i">
            <input type="text" :placeholder="`Player ${i}`" :value="getName(i)" @input="addPlayer(i, $event.target.value)"/>
        </span>
    </div>
</template>

<script>
    export default {
        name: 'PlayerName',
        data: () => ({
            players: [],
        }),
        mounted() {
            this.players = JSON.parse(sessionStorage.getItem('players')) || []
        },
        methods: {
            addPlayer(id, name) {
                this.players[id-1] = { id, name, points: this.players[id-1]?.points || 0 }
                sessionStorage.setItem('players', JSON.stringify(this.players))
            },
            getName(index) {
                if (!JSON.parse(sessionStorage.getItem('players'))) return ''

                let players = JSON.parse(sessionStorage.getItem('players'))
                return players[index-1]?.name
            }
        },
        computed: {
            count() {
                return Number(sessionStorage.getItem('player-count')) || 2
            }
        }
    }
</script>

<style scoped>
    .game-title {
        margin: 0 0 1rem 0;
        width: 100%;
    }
    .game-title,
    input {
        height: 10vh;
        font-size: 3ch;
    }

    input {
        width: 100%;
        border-bottom: 1px solid black;
        padding: 1rem;
        margin-bottom: .5rem;
    }
</style>