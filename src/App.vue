<template>
  <div id="app">
    <div class="turntable-box">
      <turntable
          :prize-all-num="8"
          :prize-index="turntableOption.prizeIndex"
          :duration="turntableOption.duration"
          :turns-number="turntableOption.turnsNumber"
          :lottery-bg="turntableOption.lotteryBg"
          :pointer-bg="turntableOption.pointerBg"
          :pointer-x-y="turntableOption.pointerXY"
          :is-start-rotate.sync="turntableOption.isStartRotate"
          @lotteryClick="lotteryClick"
          @turnDoneCb="turnDoneCb" />
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      turntableOption: {
        pointerXY: ["50%", "33%"],
        isStartRotate: 0,
        prizeIndex: 0,
        duration: 5000,
        turnsNumber: 4,
        pointerBg: "https://res.cdn.changbaimg.com/!/yunying/nationalday2020/point_btn.png",
        lotteryBg: "https://res.cdn.changbaimg.com/!/yunying/nationalday2020/turntable.png"
      }
    }
  },
  mounted() {
  },
  methods: {
    lotteryClick() {
      this.turntableOption.isStartRotate = 1;
      // parseInt(Math.random()*(maxNum-minNum+1)+minNum,10);
      this.turntableOption.prizeIndex = parseInt(Math.random() * (8 - 1 + 1) + 1, 10);
      console.log("this.prizeIndex = ", this.turntableOption.prizeIndex);
    },
    turnDoneCb() {
      alert('恭喜获得百万现金大奖')
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
}
.turntable-box {
    width: 540px;
    height: 540px;
    margin: 50px auto 0;
  }
</style>
