<script>
import Result from './Components/Result.vue';
export default {
    data() {
        return {
            showBtn: true,
            backdrop: true,
            startTime: null,
            reactionTime: null,
            buttonType: "Go",
            isGameStopped: false
        }
    },
    methods: {
        changeBackground() {
            this.storeTime = setTimeout(() => {
                this.backdrop=!this.backdrop;
                this.startTime = Date.now();
                this.isGameStopped = true;
            }, Math.floor(Math.random() * (10000 - 3000 + 1)) + 3000);
        },
        getReactionTime() {
            if (this.showBtn)
                this.buttonType = "Go";
            else
                this.buttonType = "Stop"
            if (this.buttonType === "Stop") {
                this.isGameStopped = false;
                this.changeBackground();
            }
            else {
                if (this.startTime !== null) {
                    this.reactionTime = Date.now() - this.startTime;
                    this.startTime = null;
                }
                if (this.isGameStopped === false) {
                    clearTimeout(this.storeTime);
                    this.startTime = null;
                    this.reactionTime = null;
                }
            }
        },
        updateIsGameStopped(value) {
            this.isGameStopped = value;
        },
        updateBackdrop(value){
            this.backdrop=value;
        }

    },
    components: {
        Result,
    }
}
</script>

<template>
    <div class="main-container" :class="{ 'background-color-blue': backdrop, 'background-color-green': !backdrop }">
        <div :class="[buttonType === 'Stop' ? 'card-red' : 'card-green']" id="card1"
            @click="showBtn = !showBtn, getReactionTime()">
            {{ buttonType }}
        </div>
        <Result :buttonType="buttonType" :reactionTime="reactionTime" :isGameStopped="isGameStopped"
            @update:isGameStopped="updateIsGameStopped" :backdrop="backdrop" @update:backdrop="updateBackdrop"></Result>
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

.card-green {
    background-color: rgba(86, 223, 86, 0.679);
}

.card-red {
    background-color: rgba(251, 41, 41, 0.768);
}

#card1 {
    width: 50%;
    margin: 0px auto;
    margin-top: 50px;
    height: 180px;
    border-radius: 10px;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    cursor: pointer;
    font-size: 3rem;
}

.background-color-green {
    background-color: green;
}

.background-color-blue {
    background-color: rgb(24, 187, 227);
}
</style>