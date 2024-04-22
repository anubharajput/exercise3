<script>
import Result from './Components/Result.vue';
import ShowCard from './Components/ShowCard.vue';
export default {
    data() {
        return {
            maxValue:0,
            showBtn: true,
            backdrop: true,
            reactionTime:0,
            timeDiff:0,
            showModelComponent: false,
            handleResult:0
      }
    },
    methods: {
        changeBackground() {
            setTimeout(() => {
                this.backdrop=!this.backdrop
                this.reactionTime=Date.now();
            }, Math.floor(Math.floor(Math.random() * (10000 - 3000 + 1)) + 3000));
        },
        getReactionTime(){
         this.timeDiff=Date.now()-this.reactionTime;
         console.log(this.reactionTime);
         if(this.reactionTime===0 && this.handleResult===0)
         this.handleResult=1;
         else if(this.reactionTime===0 && this.handleResult==1)
         this.handleResult=0;
        else if(this.reaction!==0)
        this.handleResult=2;
         console.log("ok");
         
         console.log(this.reactionTime);
         console.log(this.timeDiff);
        },
        showModel() {
            this.showModelComponent = !this.showModelComponent;
        }
    },
    mounted() {
        this.changeBackground();
    },
    components: {
        Result,
        ShowCard
    }
}
</script>

<template>
    <div class="main-container" :class="{'background-color-green': backdrop, 'background-color-blue': !backdrop}">
        <div :class="{ 'card': showBtn === true, 'card2': showBtn !== true} " id="card1" @click="showBtn = !showBtn , getReactionTime(),vh">
            <h1 v-if="showBtn" >Go</h1>
            <h1 v-else>Stop</h1>
        </div>
        <Result :handleResult="handleResult"
        :timeDiff="timeDiff"
        :maxValue="maxValue"
        :showModel="showModel"/>
    </div>
    <ShowCard v-if="showModelComponent" :showModel="showModel" :maxValue="maxValue"
    :timeDiff="timeDiff" />
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

.card {
    width: 60%;
    margin: auto;
    height: 200px;
    border-radius: 10px;
    background-color: rgba(86, 223, 86, 0.679);
}

.card2 {
    width: 60%;
    margin: auto;
    height: 200px;
    border-radius: 10px;
    background-color: rgba(251, 41, 41, 0.768);
}

#card1 {
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    cursor: pointer;
}
.background-color-green{
    background-color: green;
}
.background-color-blue{
    background-color: rgb(24, 187, 227);
}
</style> 




