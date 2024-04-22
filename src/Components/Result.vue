<template>
 <div class="container">
    <h4 v-if="handleResult===0">Click Go to test your reaction time!</h4>
    <h4 v-else-if="handleResult===1">Too quick... Try again!</h4>
    <h4 v-else-if="handleResult===2">Your reaction time was {{ maxValue }} seconds.</h4>
 </div>
</template>
<script>
export default{
    props:['handleResult','timeDiff','maxValue', 'showModel'],
    data()
    {
        return{
            arr:[],
            currentValue:0
        }
    },
    watch: {
    handleResult(newValue) {
        
      if (newValue === 2) {
        this.currentValue=this.timeDiff;
        if(this.arr.length===0){
        this.$emit('update:this.maxValue', this.timeDiff);
        console.log(this.maxValue);
        this.showModel();
        }
    //     this.arr.push(this.timeDiff);
    //     this.$emit('update:this.maxValue', this.timeDiff);
    //     if(this.maxValue<this.timeDiff)
    //     this.$emit('update:this.maxValue', this.timeDiff);
    // }
    // if(this.currentValue===this.maxValue && this.currentValue!=0){
    //     console.log("height score is");
    // this.showModel();
    // }
    }
  }
}
}
</script>
<style>
.container{
    width:60%;
    margin:auto;
    height:200px;
    background-color: azure;
    border-radius:10px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    }
</style>