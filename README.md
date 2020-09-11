
``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8081
npm run dev

# build for production with minification
npm run build
```

How To Use
----------------------
## 入口文件或相应vue文件引入
```bash
import Vue from 'vue'
import Turntable from 'vue-turntable'

Vue.use(Turntable)
````
## template写法

```script
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

```

## 参数解释

|参数名   |    默认值    |     用途     |
|------     | -----------   | ---------   |
|startAngle  |  0             | 初始角度
|prizeAllNum |  8          | 转盘均分为多少份
|prizeIndex  | 无             | 必填，中奖的下标（逆时针方向）
|turnsNumber | 4             | 转动的圈数
|duration | 5000        | 转动持续的时间，ms
|lotteryBg |         | 转盘背景图
|pointerBg |         | 指针背景图
|pointerXY | ["50%", "33%"]        | 指针坐标 数组[x,y]
|isStartRotate | 0        | 0不转，1为开始转动
|lotteryClick |         | 必填，点击抽奖按钮的事件 
|turnDoneCb |         | 转完后的回调函数，一般是弹出中奖后的提示



样式修改请直接覆盖class





