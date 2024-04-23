<script>
import Result from './Components/Result.vue';
import ShowCard from './Components/ShowCard.vue';

export default {
    data() {
        return {
            maxValue: 0,
            showBtn: true,
            backdrop: true,
            reactionTime: 0,
            timeDiff: 0,
            showModelComponent: false,
            handleResult: null,
            storeTime: 0,
            changeBackgroundColor: true,
            buttonType:"start",
            instructionMsz:"Click Go to test your reaction time!",
            showResult:false,
            highScore:0
        }
    },
    methods: {
        changeBackground() {
            this.storeTime = setInterval(() => {
                this.backdrop = !this.backdrop;
                this.reactionTime = Date.now();
            }, Math.floor(Math.random() * (10000 - 3000 + 1)) + 3000);
        },
        getReactionTime() {
            if(this.buttonType==='start')
            this.buttonType='stop'
        else
        this.buttonType='start'
        this.timeDiff = Date.now() - this.reactionTime;
        if(this.handleResult===0 && this.buttonType==="start" && this.timeDiff===0){
            this.instructionMsz='Click Go to test your reaction time!';
            console.log(this.timeDiff);
           }
            else if (this.reactionTime === 0 && this.buttonType==="stop")
                this.instructionMsz = "Pay attention. Click stop when the color changes.";
            else if (this.reactionTime === 0 && this.buttonType==="start")
                this.instructionMsz = "Too quick... Try again!";
            else if (this.reactionTime !== 0) {
                this.instructionMsz="your score is"
                this.changeBackgroundColor=false;
                console.log("clear");
                this.showResult=true;
        }
        },
        showModel() {
            this.showModelComponent = !this.showModelComponent;
            if(this.showModelComponent===false){
            this.changeBackgroundColor=true;
            console.log(this.changeBackgroundColor);
            }
        },
        updateMaxValue(value) {
            this.maxValue = value;
       
   
    }
    },
    watch: {
    changeBackgroundColor(newValue) {
        if (newValue === true) {
            console.log("started");
            this.handleResult=0;
            this.changeBackground(); 
            this.showResult=false;
            this.maxValue=0;
            this.timeDiff=0;
            this.reactionTime=0;
            this.instructionMsz='Click Go to test your reaction time!'

        } else {
            clearInterval(this.storeTime); 
        }
    },
   },
    components: {
        Result,
        ShowCard
    },
    mounted() {
        this.changeBackground();
    },
    

}
</script>

<template>
    <div class="main-container" :class="{'background-color-green': backdrop, 'background-color-blue': !backdrop}">
        <div :class="{ 'card': showBtn === true, 'card2': showBtn !== true} " id="card1"  @click="showBtn=!showBtn, getReactionTime()">
           {{ buttonType }}
        </div>
        <Result :instructionMsz="instructionMsz" :timeDiff="timeDiff" :maxValue="maxValue" @update:maxValue="updateMaxValue" :showModel="showModel" :showResult="showResult" :highScore="highScore"/>
    </div>
    <ShowCard v-if="showModelComponent" :showModel="showModel" :maxValue="maxValue"/>
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
    margin:0 auto;
    height: 200px;
    border-radius: 10px;
    background-color: rgba(86, 223, 86, 0.679);
}

.card2 {
    width: 60%;
    margin:  0px auto;
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




