<script>
import Result from './Components/Result.vue';
import GameBtn from './Components/GameBtn.vue';
export default {
    data() {
        return {
            changeBackgroundColor: true,
            startTime: null,
            reactionTime: null,
            buttonLabel: "Go",
            isGameStopped: false,
            currentBackgroundColor:""
        }
    },
    methods: {
        getReactionTime() {
            console.log("cvb")
            if (this.buttonLabel === "Stop") {
                this.isGameStopped = false;
                this.currentBackgroundColor = setTimeout(() => {
                this.changeBackgroundColor = !this.changeBackgroundColor;
                this.startTime = Date.now();
                this.isGameStopped = true;
            }, Math.floor(Math.random() * (10000 - 3000 + 1)) + 3000);
            }
            else {
                if (this.startTime !== null) {
                    this.reactionTime = Date.now() - this.startTime;
                    this.startTime = null;
                }
                if (this.isGameStopped === false) {
                    clearTimeout(this.currentBackgroundColor);
                    this.startTime = null;
                    this.reactionTime = null;
                }
            }
        },
        updateIsGameStopped(value) {
            this.isGameStopped = value;
        },
        updatechangeBackgroundColor(value) {
            this.changeBackgroundColor = value;
        },
        updateButtonLabel(value)
        {
            this.buttonLabel=value;
        }

    },
    components: {
        Result,
        GameBtn
    }
}
</script>

<template>
    <div class="main-container"
        :class="{ 'background-color-blue': changeBackgroundColor, 'background-color-green': !changeBackgroundColor }">
        <GameBtn :buttonLabel="buttonLabel" @update:buttonLabel="updateButtonLabel" @click="getReactionTime"/>
        <Result :buttonLabel="buttonLabel" :reactionTime="reactionTime" :isGameStopped="isGameStopped"
            @update:isGameStopped="updateIsGameStopped" :changeBackgroundColor="changeBackgroundColor"
            @update:changeBackgroundColor="updatechangeBackgroundColor"></Result>
    </div>
</template>

<style scoped>
.main-container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    font-family: sans-serif;
    width: 100%;
    height: 100vh;
}

.background-color-green {
    background-color: green;
}

.background-color-blue {
    background-color: rgb(24, 187, 227);
}
</style>