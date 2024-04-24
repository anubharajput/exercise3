<template>
  <div class="container">
    <div v-if="scoreMessage">
      Your reaction time was {{ scoreMessage }} seconds
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
  props: ["buttonType", "reactionTime", "isGameStopped","backdrop"],
  methods: {
    getHightScore() {
      this.CurrentScore = this.reactionTime
      if (this.highScore === null) {
        this.highScore = this.CurrentScore;
        this.arr.push(this.reactionTime);
      }
      else if (this.highScore > this.CurrentScore) {
        this.arr.push(this.CurrentScore);
        this.highScore = this.CurrentScore;
      }
      this.$emit("update:isGameStopped", false);
      this.$emit("update:backdrop",true);
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
      this.scoreMessage = this.CurrentScore/1000;
      this.instructionMessage = "Click Go to test your reaction time!";
      this.highScoreMessage = `Your High Score is ${this.highScore / 1000} seconds`;
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
  font-size:20px;
}
</style>