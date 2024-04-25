<script>
  import Result from "./Components/Result.vue";
  import GameBtn from "./Components/GameBtn.vue";
  export default {
    data() {
      return {
        isBackgroundcolorBlue: true,
        userStartTime: null,
        userStopTime: null,
        isStartBtn:true,
        isGameStopped: false,
        timeoutRef: "",
        currentScore: null,
        highScore: null,
      };
    },
    methods: {
      handleGoStopBtn() {
        if (!this.isStartBtn) {
          this.timeoutRef = setTimeout(() => {
            this.isBackgroundcolorBlue = !this.isBackgroundcolorBlue;
            this.userStartTime = Date.now();
            this.isGameStopped = true;
          }, 5000);
        } else {
          if (this.userStartTime !== null) {
            this.userStopTime = Date.now() - this.userStartTime;
            this.userStartTime = null;
          }
          if (this.isGameStopped === false) {
            clearTimeout(this.timeoutRef);
            this.userStartTime = null;
            this.userStopTime = null;
          }
        }
       this.getHighScore();
      },
      updateIsStartBtn(value) {
        this.isStartBtn = value;
      },
      getHighScore(){
        this.currentScore = this.userStopTime;
        if (this.highScore === null) {
          this.highScore = this.currentScore;
        } else if (this.highScore > this.currentScore) {
          this.highScore = this.currentScore;
        }
        this.isGameStopped = false;
        this.isBackgroundcolorBlue = true;
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
    :class="[isBackgroundcolorBlue?'background-color-blue':'background-color-green']">
    <GameBtn
      :isStartBtn="isStartBtn"
      @update:isStartBtn="updateIsStartBtn"
      @click="handleGoStopBtn" />
    <Result
      :isStartBtn="isStartBtn"
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