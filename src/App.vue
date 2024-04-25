<script>
  import Result from "./Components/Result.vue";
  import GameBtn from "./Components/GameBtn.vue";
  export default {
    data() {
      return {
        changeBackgroundColor: true,
        UserStartTime: null,
        userStopTime: null,
        buttonLabel: "Go",
        isGameStopped: false,
        currentBackgroundColor: "",
        currentScore: null,
        highScore: null,
      };
    },
    methods: {
      handleClick() {
        if (this.buttonLabel === "Stop") {
          this.isGameStopped = false;
          this.currentBackgroundColor = setTimeout(() => {
            this.changeBackgroundColor = !this.changeBackgroundColor;
            this.userStartTime = Date.now();
            this.isGameStopped = true;
          }, Math.floor(Math.random() * (10000 - 3000 + 1)) + 3000);
        } else {
          if (this.userStartTime !== null) {
            this.userStopTime = Date.now() - this.userStartTime;
            this.userStartTime = null;
          }
          if (this.isGameStopped === false) {
            clearTimeout(this.currentBackgroundColor);
            this.userStartTime = null;
            this.userStopTime = null;
          }
        }
       this.getHighScore();
      },
      updateButtonLabel(value) {
        this.buttonLabel = value;
      },
      getHighScore(){
        this.currentScore = this.userStopTime;
        if (this.highScore === null) {
          this.highScore = this.currentScore;
        } else if (this.highScore > this.currentScore) {
          this.highScore = this.currentScore;
        }
        this.isGameStopped = false;
        this.changeBackgroundColor = true;
      }
    },
    components: {
      Result,
      GameBtn,
    },
  };
</script>

<template>
  <div
    class="main-container"
    :class="{
      'background-color-blue': changeBackgroundColor,
      'background-color-green': !changeBackgroundColor,
    }">
    <GameBtn
      :buttonLabel="buttonLabel"
      @update:buttonLabel="updateButtonLabel"
      @click="handleClick" />
    <Result
      :buttonLabel="buttonLabel"
      :currentScore="currentScore"
      :highScore="highScore">
    </Result>
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