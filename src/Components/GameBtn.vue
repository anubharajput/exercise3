<template>
  <button :class="[isStartBtn ? 'card-green' : 'card-red']" id="card" @click="toggleBtn">
    {{ buttonText }}
  </button>
</template>

<script>
export default {
  data() {
    return {
      buttonText: "Go"
    }
  },
  props: ["isStartBtn"],
  methods: {
    toggleBtn() {
      this.$emit("update:isStartBtn", !this.isStartBtn);
      if (this.isStartBtn) this.buttonText = "stop"
      else this.buttonText = "Go"
    },
  },
};
</script>
<style scoped>
button {
  border: none;
  outline: none;
}

#card {
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

.card-green {
  background-color: rgba(86, 223, 86, 0.679);
}

.card-red {
  background-color: rgba(251, 41, 41, 0.768);
}
</style>