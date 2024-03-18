<template>
<div>
    <button @click="toggleButtonText" :style="{ backgroundColor: themeLinkColor }">{{ buttonText }}</button>
</div>
</template>

    
<script>
export default {
    name: 'GameStart',
    data() {
        return {
            buttonText: 'Go',
            gameStarted: false,
            reactionStartTime: null,
            reactionTimer: null
        }
    },
    computed: {
        themeLinkColor() {
            return this.buttonText === 'Go' ? '#68AE64' : '#C86A67';
        }
    },
    methods: {
        toggleButtonText() {
            if (this.buttonText === 'Go') {
                this.startGame();
            } else if (this.buttonText === 'Stop') {
                this.stopGame();
            }
        },
        startGame() {
            this.gameStarted = true;
            this.buttonText = 'Stop';
            const delay = Math.random() * (5000 - 2000) + 2000;
            this.reactionTimer = setTimeout(() => {
                this.reactionStartTime = performance.now();
                this.$emit('game-event', {
                    success: false,
                    message: 'Pay attention. Click stop when the color changes.'
                });
            }, delay);
        },
        stopGame() {
            if (this.reactionStartTime === null) {
                this.$emit('game-event', {
                    success: false,
                    message: 'Too quick... Try again!'
                });
            } else {
                const reactionTime = performance.now() - this.reactionStartTime;
                this.$emit('game-event', {
                    success: true,
                    time: reactionTime
                });
            }
            this.resetGame();
        },
        resetGame() {
            clearTimeout(this.reactionTimer);
            this.gameStarted = false;
            this.buttonText = 'Go';
            this.reactionStartTime = null;
        }
    }
}
</script>

<style scoped>
button {
    width: 40vw;
    height: 20vh;
    border: none;
    border-radius: 10px;
    color: #ffffff;
    font-size: 3rem;
    cursor: pointer;
}
</style>
