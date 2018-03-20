<template>
  <div>
    <div class="hello">
      <h1>{{ msg }}</h1>
    </div>

    <div class = "clock">
      <p class="time">{{time | timeFilter}}</p> 

    </div>


    <button id="play" v-on:click="play">Start</button>
    <button id="stop" v-on:click="stop">Pause</button>
    <button id="reset" v-on:click="reset">Reset</button>

  </div>


</template>


<script>

let clock;

export default {
  name: 'Timer',
  data () {
    return {
      msg: 'welcome to your meditation place.',
      time: 300,
      clockstart: false,

    }
  }, //don't forget the comma

  filters:{
    timeFilter: function (time){
      let min = Math.floor((time % 900) / 60);
      let sec = (time % 900) % 60

      if(min<10){ min = '0' + min.toString()}
      if(sec<10){ sec = '0' + sec.toString()}

      return min + ' : ' + sec;
    }
  },

  methods:{

    play: function(){

        console.log("play");

      if(this.clockstart === false){
        this.clockstart = true;

        clock = setInterval(()=> {
          if(this.time === 0 ) {
            this.stop();
          } else {
            this.time--;
          }
        }, 1000);

      }
    },

    stop: function(){
        if(this.clockstart === true){
            this.clockstart = false; 
            clearInterval(clock);
        }
    },

    reset: function(){
        this.stop();
        this.time = 300;
    }

  }

  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
.time{
  font-size: 60px
}


</style>
