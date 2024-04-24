<template>
  <div class="container">
    <div v-if="scoreMessage">
      Your reaction time was <span v-if="hours">{{ hours }} hour </span>
      <span v-if="minutes">{{ minutes }} min </span> <span v-if="seconds"> {{ seconds }} seconds</span> 0.{{ milisec }}
    </div>
    <div v-if="instructionMessage">{{ instructionMessage }}</div>
    <div v-if="highScoreMessage">{{ highScoreMessage }}</div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      instructionMessage: "Click Go to test your reaction time!",
      scoreMessage: null,
      highScoreMessage: null,
      hours: 0,
      minutes: 0,
      seconds: 0,
      milisec: 0,
      highScore: null,
      CurrentScore: null,
      arr: []
    }
  },
  props: ["buttonType", "reactionTime", "isGameStopped"],
  methods: {
    getUnitsFromTime(ms) {
      let totalSeconds = Math.floor(ms / 1000);
      const hr = Math.floor(totalSeconds / 3600);
      totalSeconds %= 3600;
      const min = Math.floor(totalSeconds / 60);
      const sec = totalSeconds % 60;
      const milisecond = ms % 1000;

      return { hr, min, sec, milisecond };
    },
    getHightScore() {
      this.CurrentScore = this.reactionTime
      if (this.arr.length === 0) {
        this.highScore = this.reactionTime;
        this.arr.push(this.reactionTime);
      }
      else if (this.highScore > this.CurrentScore) {
        this.arr.push(this.CurrentScore);
        this.highScore = this.CurrentScore;
      }
      this.$emit("update:isGameStopped", false);
    }
  },
  updated() {
    if (this.buttonType === "Stop") {
      this.instructionMessage = "Pay attention. Click stop when color changes";
      this.scoreMessage = null;
      this.highScoreMessage = null;
    } else if (this.reactionTime === null && this.buttonType === "Go") {
      this.instructionMessage = `Too quick... Try again!`;
    } else if (this.reactionTime && this.buttonType === "Go") {
      this.getHightScore();
      const { hr, min, sec, milisecond } = this.getUnitsFromTime(this.CurrentScore);
      this.scoreMessage = true;
      this.hours = hr;
      this.minutes = min;
      this.seconds = sec;
      this.milisec = milisecond;
      this.instructionMessage = "Click Go to test your reaction time!";
      this.highScoreMessage = `Your High Score is 0.${this.highScore}`;
    }
    if (this.reactionTime) {
      this.getUnitsFromTime(this.reactionTime);
    }
  },
};
</script>
<style scoped>
.container {
  width: 50%;
  margin: 0px auto;
  background-color: white;
  padding: 20px 10px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>