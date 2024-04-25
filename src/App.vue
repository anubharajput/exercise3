<script>
import Result from "./Components/Result.vue";
import GameBtn from "./Components/GameBtn.vue";
export default {
  data() {
    return {
      isBackgroundcolorBlue: true,
      userStartTime: null,
      userStopTime: null,
      //to change the lable of button
      isStartBtn: true,
      //to check game is on running stage or paused so we handle the setTimeout function
      isGameStarted: false,
      timeoutRef: "",
      highScore: null,
    };
  },
  methods: {
    handleGoStopBtn() {
      if (!this.isStartBtn) {
        this.timeoutRef = setTimeout(() => {
          this.isBackgroundcolorBlue = !this.isBackgroundcolorBlue;
          this.userStartTime = Date.now();
          this.isGameStarted = true;
        }, 5000);
      } else {
        if (this.userStartTime !== null) {
          this.userStopTime = Date.now() - this.userStartTime;
        }
        if (this.isGameStarted === false) {
          clearTimeout(this.timeoutRef);
          this.userStartTime = null;
          this.userStopTime = null;
        }
      }//to get maximum score
      if (this.highScore === null || this.userStopTime < this.highScore)
        this.highScore = this.userStopTime;
      this.isGameStarted = false;
      this.isBackgroundcolorBlue = true;
    },
    updateIsStartBtn(value) {
      this.isStartBtn = value;
    },
  },
  components: {
    Result,
    GameBtn,
  },
};
</script>

<template>
  <div class="main-container" :class="[isBackgroundcolorBlue ? 'background-color-blue' : 'background-color-green']">
    <GameBtn :isStartBtn="isStartBtn" @update:isStartBtn="updateIsStartBtn" @click="handleGoStopBtn" />
    <Result :isStartBtn="isStartBtn" :userStopTime="userStopTime" :highScore="highScore">
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