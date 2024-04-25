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
  props: ["isStartBtn", "userStopTime", "highScore"],
  updated() {
    if (!this.isStartBtn) {
      this.instructionMessage = "Pay attention. Click stop when color changes";
      this.scoreMessage = null;
      this.highScoreMessage = null;
    } else if (this.userStopTime === null && this.isStartBtn) {
      this.instructionMessage = `Too quick... Try again!`;
    } else if (this.userStopTime && this.isStartBtn) {
      this.scoreMessage = this.userStopTime / 1000;
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
  font-size: 20px;
}
</style>