<template>
    <div :key="refresh">
        <label class="game-title">Score board</label>
        <span v-for="(player, i) in players" :key="i">
            <span class="score-board" v-if="player">
                <p class="player-name">{{ player.name }}</p>
                <p class="points">
                    <span>{{ player.points }}</span>
                    <span class="btn-group">
                        <button @click="removePoint(player)">-</button>
                        <button @click="addPoint(player)">+</button>
                    </span>
                </p>
            </span>
            <p v-if="player" class="black-line"></p>
        </span>
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
    .game-title {
        width: 100%;
        height: 10vh;
        font-size: 3ch;
    }
    .btn-group {
        display: flex;
        align-items: center;
        gap: 1em;
    }
    button {
        background: grey;
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }
    .black-line {
        border-bottom: 1px solid black;
        width: 100%;
    }
    .score-board {
        margin-top: 0.7rem;
        display: flex;
        align-items: center;
        gap: 2rem;
        height: 10vh;
    }
    .score-board p {
        margin-left: 1rem;
        height: 3vh;
        font-size: 3ch;
    }
    .player-name {
        width: 40%;
    }
    .points {
        display: flex;
        gap: 1rem;
        width: 50%;
    }
    .points > * {
        display: flex;
        justify-content: center;
        align-items: baseline;
        flex-grow: 1;
    }
</style>