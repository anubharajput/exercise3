<template>
 <div class="container">
   <h4 v-if="showResult">{{instructionMsz }} 
  {{ maxValue }}</h4>
  <h4 v-else>{{ instructionMsz }}</h4>
  <h4 v-if="highScore!==0"> High Score is={{ highScore }}</h4>
 </div>
</template>
<script>
export default{
    props:['instructionMsz','timeDiff','maxValue', 'showModel','showResult','highScore'],
    data()
    {
        return{
            arr:[],
            currentValue:0
        }
    },
    watch: {
    timeDiff(newValue) {
        
      if (this.showResult) {
        if(this.arr.length===0){
        this.currentValue=this.timeDiff;
        this.$emit('update:maxValue', this.timeDiff);
        this.showModel();
        }
        else if(this.currentValue<this.timeDiff)
        {
          this.$emit('update:maxValue', this.timeDiff-this.maxValue);
          this.currentValue=this.timeDiff
        }
    }
  }
}
}
</script>
<style>
.container{
    width:60%;
    margin:0px auto;
    height:200px;
    background-color: azure;
    border-radius:10px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    }
</style>