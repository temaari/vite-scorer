<template>
    <div class="t-player-item" :key="refresh">
        <label class="t-name">Score board</label>
        <div class="t-player-names">
            <span v-for="(player, i) in players" :key="i">
                <span class="t-player" v-if="player">
                    <p class="grid-col-span-3">{{ player.name }}</p>
                    <p class="horizontal-center">{{ player.points }}</p>
                    <button @click="removePoint(player)">-</button>
                    <button @click="addPoint(player)">+</button>
                </span>
            </span>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'GameStart',
        data: () => ({ refresh: 0 }),
        methods: {
            addPoint(player) {
                let players = this.players
                players[player.id-1].points++
                this.refresh++
                this.gameChanges(players)
            },
            removePoint(player) {
                let players = this.players
                if (players[player.id-1].points > 0) players[player.id-1].points--
                this.refresh++
                this.gameChanges(players)
            },
            gameChanges(players) {
                sessionStorage.setItem('players', JSON.stringify(players))
            }
        },
        computed: {
            players() {
                return JSON.parse(sessionStorage.getItem('players')) || []
            }
        }
    }
</script>

<style scoped>
    .t-player-item {
        width: 100%;
        display: flex;
        min-height: 40vh;
        flex-direction: column;
        justify-content: center;
        align-items: left;
        font-size: 6ch;
    }
    .t-name {
        width: 100%;
        display: flex;
        justify-content: center;
    }
    .t-player-names {
        display: grid;
        gap: 1rem;
        grid-template-columns: repeat(3, 1fr);
    }
    .t-player-names > * {
        max-height: 8vh;
        min-height: 6vh;
    }
    .t-player {
        display: grid;
        grid-template-columns: repeat(6, 1fr);
        gap: 1;
    }
    .horizontal-center {
        display: flex;
        justify-content: center;
    }
    .grid-col-span-3 {
        grid-column: span 3;
    }
    .t-player button {
        border-radius: 100%;
        width: 90%;
        height: 100%;
        font-size: 1ch;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    @media only screen and (max-width: 700px) {
        .t-player-item {
            min-height: 100vh;
        }
        .t-player-names {
            min-height: 30vh;
            grid-template-columns: repeat(1, 1fr);
            gap: 1rem;
            margin-bottom: 1rem;
        }
        .t-player {
            padding-bottom: 0.5rem;
            margin-bottom: 0.5rem;
            border-bottom: 1px solid black;
        }
    }
</style>