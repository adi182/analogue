<template>
  <div class="vue-clock">
    <div ref="circleContainer" class="circleContainer">
      <div ref="tickFull" class="tickFull tick tickVertical"></div>
      <div ref="tickQuarter" class="tickQuarter tick tickSide"></div>
      <div ref="tickHalf" class="tickHalf tick tickVertical"></div>
      <div ref="tickThreeQuarter" class="tickThreeQuarter tick tickSide"></div>
      <div ref="hourHand" class="hourHand hand"></div>
      <div ref="minuteHand" class="minuteHand hand"></div>
      <div ref="secondHand" class="secondHand hand"></div>
      <div ref="handDot"></div>
      <div class="popper" v-show="showPopper">{{ popperText }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueClock',
  data() {
    return {
      showPopper: false,
      popperText: '',
      hourHand: null,
      minuteHand: null,
      secondHand: null,
      percent: null,
      halfMinuteMessage: null
    }
  },
  mounted(){
    this.hourHand = this.$refs.hourHand;
    this.minuteHand = this.$refs.minuteHand;
    this.secondHand = this.$refs.secondHand;
    this.halfMinuteMessage = prompt('Please enter a half minute message');
    this.timer = setInterval(() => {
        this.updateTime()
      }, 1000)
  },
  methods:{
    toast(text) {
        this.showPopper = true;
        this.popperText = text;
        setInterval(()=> {
          this.showPopper = false;
        }, 3000)
    },
    setClockFingers(dateTime){
      const htime = dateTime.getHours();
      const mtime = dateTime.getMinutes();
      const stime = dateTime.getSeconds();
      const hrotation = 30*htime + mtime/2;
      const mrotation = 6*mtime;
      const srotation = 6*stime;
      this.hourHand.style.transform = `rotate(${hrotation}deg)`;
      this.minuteHand.style.transform = `rotate(${mrotation}deg)`;
      this.secondHand.style.transform = `rotate(${srotation}deg)`;
    },
    checkAlerts(dateTime){
      if(dateTime.getSeconds() % 30 == 0) {
        this.toast('Half a minute has gone by ' + this.halfMinuteMessage)
      }
      switch(dateTime.getHours()) {
        case 1:
          this.toast('Its currently 1pm')
          break;
        case 5:
          this.toast('Its currently 5pm')
          break
      }
    },
    updateTime() {
      const dateTime = new Date();
      this.setClockFingers(dateTime);
      this.checkAlerts(dateTime)
    }
 },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .circleContainer {
      border: 1px solid black;
      border-radius: 100%;
      width: 300px;
      height: 300px;
      position: relative;
    }

    .handDot {
      position: absolute;
      left: calc(50% - 7px);
      top: calc(50% - 7px);
      width: 15px;
      height: 15px;
      border-radius: 100%;
      background: red;
      z-index: 1;
    }

    .circleContainer > .hand {
      width: 1px;
      background: blue;
      z-index: 1;
      position: absolute;
      left: 50%;
      transform-origin: bottom;
    }

    .hourHand {
      height: 40%;
      width: 10px;
      top: 10%;
    }

    .minuteHand {
      height: 30%;
      top: 20%;
    }

    .secondHand {
      height: 30%;
      top: 20%;
    }

    .circleContainer > .tick {
      height: 15px;
      width: 1px;
      background: red;
      position: absolute;
    }
    .circleContainer > .tick.tickVertical {
      left: 50%;
    }

    .circleContainer > .tick.tickSide {
      transform: rotate(90deg);
      top: calc(50% - 7px);
    }

    .tickFull {
      top: 0;
    }
    .tickQuarter {
      right: 7px;
    }
    .tickHalf {
      bottom: 0;
    }
    .tickThreeQuarter {
      left: 7px;
    }

    .popper {
      position: absolute;
      left: 5px;
      bottom: 5px;
      background: red;
      color: white;
      padding: 32px;
    }

</style>
