<template>
    <div class="content-flex-box">
        <div class="content-flex-item">
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
    }
    .s-player-names {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 0.3rem;
        min-height: 20vh;
    }
    .s-player-names > * {
        max-height: 6vh;
        min-height: 4rem;
    }
    @media only screen and (max-width: 700px) {
        .s-player-names {
            min-height: 30vh;
            grid-template-columns: repeat(2, 1fr);
            gap: 0;
        }
    }
    @media only screen and (max-width: 400px) {
        .s-player-names {
            min-height: 30vh;
            grid-template-columns: repeat(1, 1fr);
            gap: 0;
        }
    }
</style>