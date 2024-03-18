<template>
<div class="container">
    <GameStart @game-event="handleGameEvent" />
    <GameResult :result="gameResult" :highScore="highScore" />
</div>
</template>

  
  
<script>
import GameStart from './components/GameStart.vue'
import GameResult from "./components/GameResult.vue"

export default {
    name: 'App',
    components: {
        GameStart,
        GameResult
    },
    data() {
        return {
            gameResult: null,
            highScore: Infinity,
        };
    },
    methods: {
        handleGameEvent(event) {
            if (event.success) {
                this.gameResult = `Your reaction time: ${event.time.toFixed(2)} ms`;
                if (event.time < this.highScore) {
                    this.highScore = event.time;
                }
            } else {
                this.gameResult = event.message;
            }
        }
    }
}
</script>

<style scoped>
body {
    margin: 0;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    display: flex;
    height: 100vh;
    align-items: center;
    justify-content: center;
}

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>
