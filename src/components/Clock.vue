<template>
  <div class="clock">
    <div class="container">
      <div class="column has-text-centered">
        <h1 class="title">Pomodoro Clock</h1>
      </div>
      <div class="columns">
        <div class="column">
          <div class="column">
            <h1>Break Time</h1>
          </div>
          <div class="column">
              <b-numberinput v-model="breakTime" editable=false :min="5" :max="25"></b-numberinput>
          </div>
        </div>
        <div class="column">
          <div class="column">
            <h1>Session Time</h1>
          </div>
          <div class="column">
            <b-numberinput v-model="sessionTime" editable=false :min="1" :max="60"></b-numberinput>
          </div>
        </div>
      </div>
      <div class="column">
        <div class="tile notification is-info" style="border-radius: 3.50em;">
          <div class="column">
            <p class="title" style="margin: auto">Timer:</p>
          </div>
          <div class="column">
            <p class="title"><span id="minutes">{{ minutes }}</span>
              <span id="middle">:</span>
              <span id="seconds">{{ seconds }}</span></p>
          </div>
        </div>
      </div>
      <div class="column">
        <a @click="this.startTimer"><b-icon icon="play-circle" size="is-large" style="color: #187DF0"></b-icon></a>
        <a @click="this.stopTimer"><b-icon icon="pause-circle" size="is-large" style="color: #187DF0"></b-icon></a>
        <a @click="this.resetTimer"><b-icon icon="stop-circle" size="is-large" style="color: #187DF0"></b-icon></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  data(){
    return {
      sessionTime: 25,
      breakTime: 5,
      timer: null,
      totalTime: null,
      resetButton: false,
    }
  },
  mounted() {
    this.totalTime = (25 * 60);
  },
  watch: {
    sessionTime: function (){
      console.log(this.sessionTime)
      this.totalTime = (this.sessionTime * 60);
    },
    totalTime: function (){
      if(this.totalTime === 0){
        this.totalTime = (this.breakTime * 60);
      }
    }
  },
  methods: {
    startTimer: function() {
      this.timer = setInterval(() => this.countdown(), 1000);
      this.resetButton = true;
    },
    stopTimer: function() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
    },
    resetTimer: function() {
      this.totalTime = (this.sessionTime * 60);
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
    },
    padTime: function(time) {
      return (time < 10 ? '0' : '') + time;
    },
    countdown: function() {
      this.totalTime--;
    }
  },
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function() {
      const seconds = this.totalTime - (this.minutes * 60);
      return this.padTime(seconds);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
