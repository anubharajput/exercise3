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
    }
  },
  props: ["buttonLabel", "currentScore","highScore"],
  updated() {
    if (this.buttonLabel === "Stop") {
      this.instructionMessage = "Pay attention. Click stop when color changes";
      this.scoreMessage = null;
      this.highScoreMessage = null;
    } else if (this.currentScore === null && this.buttonLabel === "Go") {
      this.instructionMessage = `Too quick... Try again!`;
    } else if (this.currentScore && this.buttonLabel === "Go") {
      this.scoreMessage = this.currentScore/1000;
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