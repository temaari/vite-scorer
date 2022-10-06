<template>
    <div class="game-window">
        <div class="game-content">
            <get-started v-if="currentPage === Page.Start" />
            <player-counter v-if="currentPage === Page.PlayerCount" />
            <player-name v-if="currentPage === Page.PlayerName" />
            <game-start v-if="currentPage === Page.Game" />
        </div>
        <game-buttons class="game-buttons"
            :showPrev="currentPage !== Page.Start"
            :showNext="currentPage !== Page.Game"
            @clickedPrev="goLeft"
            @clickedNext="goRight"
        />
    </div>
</template>

<script>
    import GetStarted from './components/GetStarted.vue'
    import PlayerCounter from './components/PlayerCounter.vue'
    import PlayerName from './components/PlayerName.vue'
    import GameStart from './components/GameStart.vue'
    import GameButtons from './components/GameButtons.vue'
    import { Page } from './helpers/Enums'

    export default {
        name: 'Scorer',
        components: {
            GetStarted,
            PlayerCounter,
            PlayerName,
            GameStart,
            GameButtons
        },
        data: () => ({
            Page,
            currentPage: Page.Start,
            startX: 0,
            startY: 0,
            endX: 0,
            endY: 0
        }),
        computed: {
        },
        mounted() {
            this.loadFromSessionStorage()

            // event listeners for left right swipe
            document.addEventListener('touchstart', this.startSwipe)
            document.addEventListener('touchend', this.handleSwipe)
        },
        methods: {
            startSwipe(e) {
                this.startX = e.changedTouches[0].pageX
                this.startY = e.changedTouches[0].pageY
            },
            handleSwipe(e) {
                this.endX = e.changedTouches[0].pageX
                this.endY = e.changedTouches[0].pageY

                if (this.startX > this.endX) {
                    // go right
                    if (this.withinYRange() && this.startX > this.endX + 50) this.goRight()
                } else {
                    // go left
                    if (this.withinYRange() && this.startX < this.endX - 50) this.goLeft()
                }
            },
            goLeft() {
                if (this.currentPage !== 0) this.goto(this.currentPage-1)
            },
            goRight() {
                if (this.currentPage !== 3) this.goto(this.currentPage+1)
            },
            withinYRange() {
                return (this.endY > this.startY - 50 && this.endY < this.startY + 50)
            },
            goto(page) {
                sessionStorage.setItem('page', page)
                this.getSaveData()
            },
            getSaveData() {
                this.currentPage = Number(sessionStorage.getItem('page'))
            },
            loadFromSessionStorage() {
                if (sessionStorage.getItem('game-in-progress') === null) {
                    sessionStorage.setItem('game-in-progress', true)
                } else {
                    this.getSaveData()
                }
            }
        }
    }
</script>

<style>
    .game-window {
        min-height: 40vh;
        max-width: 60%;
        margin: 0 auto;
        margin-top: 15vh;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        background: lightcyan;
    }
    .game-content {
        min-height: 40vh;
    }
    .game-buttons {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
    }
    .content-flex-box {
        height: 40vh;
        width: 100%;
        display: flex;
        align-items: center;
    }
    .content-flex-item {
        width: 100%;
        font-size: 6ch;
        display: flex;
        justify-content: center;
    }
    .btn-reset {
        grid-column: span 2;
    }
    @media only screen and (max-width: 700px) {
        .game-window {
            max-width: 100%;
            padding: 0;
            margin-top: 0;
            min-height: 100vh;
        }
        .game-content {
            min-height: 78vh;
        }
        .game-buttons {
            gap: 0.2;
        }
        .content-flex-item {
            font-size: 6ch;
        }
    }
</style>