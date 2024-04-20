<script>
import Result from './Components/Result.vue'
export default {
    data() {
        return {
            showBtn: true,
        }
    },
    methods: {
        getRandomTime() {
            console.log(Math.floor(Math.random() * 3000) + 2000);
            return Math.floor(Math.random() * 3000) + 2000;
        }
    },
    components: {
        Result
    }
}
</script>

<template>
    <div class="main-container">
        <div :class="{ 'card': showBtn === true, 'card2': showBtn !== true }" id="card1" @click="showBtn = !showBtn">
            <h1 v-if="showBtn">Go</h1>
            <h1 v-else>Stop</h1>
        </div>
        <Result />
    </div>
</template>

<style scoped>
.main-container {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    gap: 20px;
    font-family: sans-serif;
}

.card {
    width: 60%;
    margin: auto;
    height: 200px;
    border-radius: 10px;
    background-color: rgba(86, 223, 86, 0.679);
}

.card2 {
    width: 60%;
    margin: auto;
    height: 200px;
    border-radius: 10px;
    background-color: rgba(251, 41, 41, 0.768);
}

#card1 {
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    cursor: pointer;
}
</style>
