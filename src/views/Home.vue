<template>
  <div class="home">
    <div class="text__outer">
      <div class="text__inner">
        
        <div class="currentNumber__outer">
          <p class="description">Huidige nummer</p>
          <h1 class="amount">{{ currentNumber }}</h1>
        </div>

        <button 
        class="increase__btn"
          @click="increaseCurrentNumber()"
          v-on:keyup.enter="increaseCurrentNumber()"
          >Volgende</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "home",
  components: {
  },
  data() {
    return {
      currentNumber: 1
    }
  },
  methods:{
    increaseCurrentNumber(){
       this.currentNumber = this.currentNumber + 1;
    },
 doCommand(e) {
    let cmd =e.keyCode;
    if(cmd === 13 || cmd === 32){
      this.increaseCurrentNumber();
    }
	}
  },
  mounted(){
    if(this.$route.params.id === 'rnd'){
      this.currentNumber = Math.floor((Math.random() * 1000) + 1);
    }
    else if(this.$route.params.id && Number(this.$route.params.id) && this.$route.params.id > this.currentNumber){
      this.currentNumber = Number(this.$route.params.id);
    }
  },
  created() {
	  window.addEventListener('keypress', this.doCommand);
  },
  destroyed() {
    window.removeEventListener('keypress', this.doCommand);
  },
};
</script>

<style lang="scss" scoped>
.text__outer{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background: #f0f0f0
}

.text__inner{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.currentNumber__outer{
  margin-bottom: 40px;
  width: 90vw;
  height: 90vw;
  max-width: 350px;
  max-height: 350px;
  border-radius: 5px;
  background: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.description{
  font-weight: normal;
  font-size: 14px;
  color: #333333;
   margin: 0;
}
.amount{
  font-weight: normal;
  font-size: 64px;
  color: #ff6200;
  font-weight: bold;
  margin: 20px;
}

.increase__btn{
  min-width: 150px;
  min-height: 40px;
  font-size: 14px;
  font-weight: bold;
  line-height: 1.33;
  text-align: center;
  border-radius: 5px;
  padding: 5px 10px;
  background: #ff6200;
  color: #fff;
}
</style>