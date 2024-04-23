<template>
    <div>
        <div class="backdrop-container" @click="showModel()"></div>
        <div class="card-container">
            <div class="logo"><img src="https://static-00.iconduck.com/assets.00/alert-circle-icon-2048x2046-3lb5oi0m.png" alt=""></div>
            <h2>Winner!!</h2>
            <p>Your score of {{ maxValue}} has been stored in your browser and could be lost when you leave. Create an
                account or login to automatically save them to your account!</p>
            <button @click="showModel()">Got it!!</button>
        </div>
    </div>
</template>
<style scoped>
.card-container {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    background-color: white;
    padding: 20px;
    width: 30%;
    margin:0px auto;
    top: 200px;
    border-radius: 10px;
    z-index: 2;
}

.logo {
    height: 50px;
    width: 50px;
}

.logo img {
    width: 100%;
}

.backdrop-container {
    position: absolute; 
    inset: 0;
    width: 100%;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.7);
    cursor: pointer;
}
</style>

<script>
export default {
    props: ['showModel','maxValue'],

};
</script>