<template>
  <div class="watch_block">
      <div class="watch_clock-face" :class="{'active' : init}">

        <div class="watch_item"  v-if="hours">{{hours}}</div>
        <div v-if="hours">:</div>
        <div class="watch_item" v-if="min">{{min}}</div>
        <div v-if="min">:</div>
        <div class="watch_item" >{{sec}}</div>

      </div>
      <div class="watch_line" :class="{'active' : init}"></div>
      <div class="watch_buttons">
        <button @click="startPauseSW" :class="activeClass" class="button"></button>
        <button @click="resetSW" class="button watch_stop" :class="{'active' : init}"></button>
      </div>
  </div>
</template>

<script>
  export default {
    name: "Stopwatch",
    data: () => ({
      base: 60,
      init: false,
      hours: null,
      min: null,
      sec: '00',
      initialTimeStamp: null,
      tick: 0,
      timeout: null,
      activeClass: 'watch_run'
    }),
    methods: {
      startPauseSW() {
        if(this.init === false) {
          this.initialTimeStamp = new Date().getTime() - (this.tick * 1000);
          this.runSW();
          this.init = true;
          this.activeClass = 'watch_pause';
        } else {
          this.suspendTimeout();
        }
      },
      runSW() {
        const currentTimeStamp = new Date().getTime();
        this.tick = (currentTimeStamp - this.initialTimeStamp) / 1000;
        this.sec = Math.floor(this.tick);
        this.sec = this.sec % this.base;
        this.min = Math.floor(this.tick / this.base);
        this.min = this.min % this.base;
        this.hours = Math.floor(this.tick / this.base ** 2);
        if(this.sec < 10) this.sec = '0' + this.sec;
        if(this.min < 10 && this.tick >= this.base) this.min = '0' + this.min;

        this.timeout = setTimeout(this.runSW, 10);
      },
      suspendTimeout() {
        clearTimeout(this.timeout);
        this.init = false;
        this.activeClass = 'watch_run';
      },
      resetSW() {
        this.suspendTimeout();
        this.tick = 0;
        this.min = this.hours = null;
        this.sec = '00';
      },
    }
  }
</script>

<style scoped lang="scss">
  $enabled: #fff;
  $disabled: #9E9E9E;
  $background: #696969;

  .watch_ {
    &block {
      width: 225px;
      height: 120px;
      background: $background;
      display: flex;
      flex-direction: column;
      justify-content: space-evenly;
    }
    &item {
      width: 31px;
      &:first-child {
        width: auto;
        text-align: right;
      }
      &:nth-child(2) {
        text-align: center;
      }
      &:last-child {
        text-align: left;
      }
    }
    &clock-face {
      font-size: 22px;
      display: flex;
      justify-content: center;
      color: $disabled;
      &.active {
        color: $enabled;
      }
    }
    &line {
      height: 1px;
      border: none;
      background-color: $disabled;
      &.active {
        background-color: $enabled;
      }
    }
    &buttons {
      display: flex;
      justify-content: space-evenly;
      padding: 0 25px;
    }
    &run {
      &:after {
        content: '';
        position: absolute;
        top: 0;
        left: 2px;
        border: 10px solid transparent;
        border-left: 17px solid $disabled;
      }
    }
    &pause {
      &:before {
        content: '';
        position: absolute;
        top: 0;
        left: 5px;
        height: 20px;
        width: 3px;
        background-color: $enabled;
      }
      &:after {
        content: '';
        position: absolute;
        top: 0;
        right: 5px;
        height: 20px;
        width: 3px;
        background-color:  $enabled;
      }
    }
    &stop {
      background-color: $disabled;
      &.active {
        background-color: $enabled;
      }
    }
  }

</style>