<template>
    <button
      :class="[buttonLabel === 'Stop' ? 'card-red' : 'card-green']"
      id="card1"
      @click="toggleBtn">
      {{ buttonLabel }}
    </button>
  </template>
  
  <script>
    export default {
      props: ["buttonLabel"],
      methods: {
        toggleBtn() {
          if (this.buttonLabel==="Stop") this.$emit("update:buttonLabel", "Go");
          else this.$emit("update:buttonLabel", "Stop");
        },
      },
    };
  </script>
  <style scoped>
    button {
      border: none;
      outline: none;
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
    .card-green {
      background-color: rgba(86, 223, 86, 0.679);
    }
    .card-red {
      background-color: rgba(251, 41, 41, 0.768);
    }
  </style>