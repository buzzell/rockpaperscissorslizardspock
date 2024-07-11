<template>
    <main>
        <div class="game-table">
            <div class="cardbox dealer">
                <Icon v-if="computer_pick == 'rock'" :icon="faHandBackFist" />
                <Icon v-if="computer_pick == 'paper'" :icon="faHand" />
                <Icon v-if="computer_pick == 'scissors'" :icon="faHandScissors" />
                <Icon v-if="computer_pick == 'lizard'" :icon="faHandLizard" />
                <Icon v-if="computer_pick == 'spock'" :icon="faHandSpock" />
            </div>
            <div class="status" v-html="game_status"></div>
            <div class="cardbox player">
                <Icon v-if="player_pick == 'rock'" :icon="faHandBackFist" />
                <Icon v-if="player_pick == 'paper'" :icon="faHand" />
                <Icon v-if="player_pick == 'scissors'" :icon="faHandScissors" />
                <Icon v-if="player_pick == 'lizard'" :icon="faHandLizard" />
                <Icon v-if="player_pick == 'spock'" :icon="faHandSpock" />
            </div>
        </div>

        <div class="playerActions">
            <button @click="pick('rock')">
                <Icon :icon="faHandBackFist" />
                <span>ROCK</span>
            </button>
            <button @click="pick('paper')">
                <Icon :icon="faHand" />
                <span>PAPER</span>
            </button>
            <button @click="pick('scissors')">
                <Icon :icon="faHandScissors" />
                <span>SCISSORS</span>
            </button>
            <button @click="pick('lizard')">
                <Icon :icon="faHandLizard" />
                <span>LIZARD</span>
            </button>
            <button @click="pick('spock')">
                <Icon :icon="faHandSpock" />
                <span>SPOCK</span>
            </button>
        </div>
    </main>
</template>

<script setup>
import { ref } from 'vue'

import { FontAwesomeIcon as Icon } from '@fortawesome/vue-fontawesome'
import { faHandBackFist, faHand, faHandScissors, faHandLizard, faHandSpock } from '@fortawesome/free-solid-svg-icons'

const player_pick = ref(null)
const computer_pick = ref(null)
const game_status = ref('')

const symbolsarr = ['rock', 'paper', 'scissors', 'lizard', 'spock']

function pick(pp) {
    player_pick.value = pp
    computer_pick.value = computerPick()

    if (player_pick.value == computer_pick.value) {
        game_status.value = 'Draw'
        return
    }

    if (player_pick.value == 'rock') {
        if (computer_pick.value == 'paper') {
            game_status.value = 'You <span class="lose">lose</span>. Paper covers rock.'
        } else if (computer_pick.value == 'scissors') {
            game_status.value = 'You <span class="win">win</span>. Rock crushes scissors.'
        } else if (computer_pick.value == 'lizard') {
            game_status.value = 'You <span class="win">win</span>. Rock crushes lizard.'
        } else if (computer_pick.value == 'spock') {
            game_status.value = 'You <span class="lose">lose</span>. Spock vaporizes rock.'
        }
    } else if (player_pick.value == 'paper') {
        if (computer_pick.value == 'rock') {
            game_status.value = 'You <span class="win">win</span>. Paper covers rock.'
        } else if (computer_pick.value == 'scissors') {
            game_status.value = 'You <span class="lose">lose</span>. Scissors cut paper.'
        } else if (computer_pick.value == 'lizard') {
            game_status.value = 'You <span class="lose">lose</span>. Lizard eats paper.'
        } else if (computer_pick.value == 'spock') {
            game_status.value = 'You <span class="win">win</span>. Paper disproves Spock.'
        }
    } else if (player_pick.value == 'scissors') {
        if (computer_pick.value == 'paper') {
            game_status.value = 'You <span class="win">win</span>. Scissors cuts paper.'
        } else if (computer_pick.value == 'rock') {
            game_status.value = 'You <span class="lose">lose</span>. Rock crushes scissors.'
        } else if (computer_pick.value == 'lizard') {
            game_status.value = 'You <span class="win">win</span>. Scissors decapitates lizard.'
        } else if (computer_pick.value == 'spock') {
            game_status.value = 'You <span class="lose">lose</span>. Spock smashes scissors.'
        }
    } else if (player_pick.value == 'lizard') {
        if (computer_pick.value == 'paper') {
            game_status.value = 'You <span class="win">win</span>. Lizard eats paper.'
        } else if (computer_pick.value == 'scissors') {
            game_status.value = 'You <span class="lose">lose</span>. Scissors decapitates lizard.'
        } else if (computer_pick.value == 'rock') {
            game_status.value = 'You <span class="lose">lose</span>. Rock crushes lizard.'
        } else if (computer_pick.value == 'spock') {
            game_status.value = 'You <span class="win">win</span>. Lizard poisons Spock.'
        }
    } else if (player_pick.value == 'spock') {
        if (computer_pick.value == 'paper') {
            game_status.value = 'You <span class="lose">lose</span>. Paper disproves Spock.'
        } else if (computer_pick.value == 'scissors') {
            game_status.value = 'You <span class="win">win</span>. Spock smashes scissors.'
        } else if (computer_pick.value == 'lizard') {
            game_status.value = 'You <span class="lose">lose</span>. Lizard poisons Spock.'
        } else if (computer_pick.value == 'rock') {
            game_status.value = 'You <span class="win">win</span>. Spock vaporizes rock.'
        }
    }
}

function computerPick() {
    return symbolsarr[Math.floor(Math.random() * (4 - 0 + 1)) + 0]
}
</script>

<style scoped lang="scss">
main {
    height: 100%;
    height: 100%;
    overflow: auto;
    display: flex;
    flex-direction: column;
}

.game-table {
    padding: 0 1rem;
    margin: auto 0;

    .cardbox {
        display: flex;
        align-items: center;
        justify-content: center;
        min-height: 10.5rem;
        padding: 1rem 0;
        flex: 1;
        font-size: 2.5rem;
    }

    .status {
        height: 1rem;
        text-align: center;
    }
}

.playerActions {
    display: flex;
    justify-content: center;
    align-items: center;

    &.isNotMobile button span::first-letter {
        font-weight: bold;
        font-size: 0.85rem;
    }

    button {
        font-size: 1.5rem;
        padding: 0.35rem;
        margin: 0 0.35rem;
        background: none;
        border: none;
        box-shadow: none;
        svg {
        }
        span {
            display: block;
            font-size: 0.75rem;
        }
    }
}
</style>
