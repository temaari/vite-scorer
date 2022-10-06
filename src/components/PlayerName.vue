<template>
    <div class="player-item">
        <label class="s-name">Enter names</label>
        <div class="s-player-names">
            <input
                v-for="i in count" :key="i"
                type="text"
                :class="'player-' + i"
                :placeholder="`Player ${i}`"
                :value="getName(i)"
                @input="addPlayer(i, $event.target.value)"
            />
        </div>
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
    .player-item {
        width: 100%;
        display: flex;
        min-height: 40vh;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        font-size: 6ch;
    }
    .s-name {
        width: 100%;
        display: flex;
        justify-content: center;
    }
    .s-player-names {
        width: 100%;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 0.3rem;
        min-height: 20vh;
    }
    .s-player-names > * {
        font-size: 0.8ch;
        max-height: 8vh;
        min-height: 6vh;
    }
    @media only screen and (max-width: 700px) {
        .player-item {
            min-height: 80vh;
            align-items: baseline;
        }
        .s-name {
            justify-content: center;
        }
        .s-player-names {
            min-height: 30vh;
            grid-template-columns: repeat(2, 1fr);
            gap: 0;
        }
        .s-player-names > * {
            font-size: 0.5ch;
            max-height: 6vh;
        }
    }
</style>