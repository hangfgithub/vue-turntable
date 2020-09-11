<template>
  <div class="turntable-wrap">
    <div
      class="turntable"
      :style="{
        transform: `rotate(${angle}deg)`,
        background: `url(${lotteryBg}) no-repeat`,
        backgroundSize: `100% 100%`,
        transition: `transform ${duration / 1000}s` }"
    ></div>
    <button
      :style="{
        left: pointerXY[0],
        top: pointerXY[1],
        background: `url(${pointerBg}) no-repeat`,
        backgroundSize: `100% 100%` }"
      class="pointer"
      @click="start"
    ></button>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Turntable",
  props: {
    //   开始的角度
    startAngle: {
      type: Number,
      default: 0
    },
    // 总共被分为多少份
    prizeAllNum: {
      type: Number,
      required: true
    },
    // 中奖的下标（逆时针方向）
    prizeIndex: {
      type: Number,
      required: true
    },
    // 转动的圈数
    turnsNumber: {
      type: Number,
      default: 4
    },
    duration: {
      type: Number,
      default: 5000
    },
    // 转盘背景
    lotteryBg: {
      type: String,
      default: function() {
        return "https://cbshowhot.cdn.changbaimg.com/!/yunying/mid-autumn-festival/turntable.png";
      }
    },
    // 指针背景
    pointerBg: {
      type: String,
      default: function() {
        return "https://cbshowhot.cdn.changbaimg.com/!/yunying/mid-autumn-festival/arrow.png";
      }
    },
    // 指针的位置
    pointerXY: {
      type: Array,
      default: function() {
        return ["50%", "33%"];
      }
    },
    // 是否开始转
    isStartRotate: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      angle: this.startAngle,
      isRolling: false
    };
  },
  watch: {
    //   监听isStartRotate值，为1时，调用转动方法
    isStartRotate() {
      if (this.isStartRotate >= 1) {
        this.startRotate();
      }
    }
  },
  methods: {
    start() {
      this.$emit("lotteryClick");
    },
    startRotate() {
      // 如果正在转，不进行任何操作 return
      if (this.isRolling) {
        return
      }
      this.isRolling = true

      const preDeg = this.angle;
      // 先转完上一次抽奖剩余的角度，在转四圈+奖品角度
      const degRotate =
        360 - (preDeg % 360) +
        360 * this.turnsNumber +
        (this.prizeIndex / this.prizeAllNum) * 360;
      this.angle += degRotate;
      console.log('this.turnsNumber', this.turnsNumber)
      setTimeout(() => {
        this.$emit('update:isStartRotate', 0)
        this.$emit('turnDoneCb')
        this.isRolling = false
      }, this.duration + 500)

    }
  }
};
</script>

<style lang="scss" scoped>
$url: "https://cbshowhot.cdn.changbaimg.com/!/yunying/mid-autumn-festival";

.turntable-wrap {
  width: 100%;
  height: 100%;
  margin: 0 auto;
  position: relative;

  .turntable {
    width: 100%;
    height: 100%;
    // background: url("#{$url}/turntable_bg.png") no-repeat;
    background: url("#{$url}/turntable.png?v=0.0.6") no-repeat;
    background-size: 100% 100%;
    transition: transform 5s ease-in-out;
  }

  .pointer {
    border: none;
    appearance: none;
    outline: none;
    background: none;
    position: absolute;
    width: 122px;
    height: 154px;
    transform: translateX(-50%);

  }
}
</style>
