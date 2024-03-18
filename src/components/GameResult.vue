<template>
<div class="result-box">
    <p v-if="result" class="result">{{ result }}</p>
    <p v-else>Click Go to test your reaction time!</p>
</div>
</template>

    
<script>
export default {
    name: 'GameResult',
    props: {
        result: String,
        highScore: Number
    }
}
</script>

    
<style scoped>
.result-box {
    background-color: #D9EDF7;
    width: 40vw;
    height: 20vh;
    margin-top: 30px;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.result {
    font-size: 1.4rem;
    text-align: center;
}
</style>
