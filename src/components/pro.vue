
<template>
  <div class="progress_box">
    <div class="inner_box">
      <div class="progress_circle position_view">
        <div class="p_left">
          <div class="left_mask" :style="{transform: 'rotate('+rotate2+'deg)'}"></div>
        </div>
        <div class="p_right">
          <div class="right_mask" :style="{transform: 'rotate('+rotate1+'deg)'}"></div>
        </div>
      </div>
      <div class="mask_circle position_view"></div>
      <div class="progress_txt">
        <div>
          <div class="progress_info">
            <span class="txt">{{progress_txt}}</span>
            <span>%</span>
          </div>
          <!-- <span class="text-gray" :style="{fontSize:13 + 'px'}"></span> -->
        </div>
      </div>
      <div class="yuanpan">
        <div
          class="kedu"
          v-for="(item,index) in 100"
          :key="index"
          :style="{transform: 'rotate('+item*10+'deg)'}"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rotate1: 180,
      rotate2: 180,
      progress_txt:100,
      time:10
    };
  },
  mounted() {
    this.draw()
  },
//   watch: {
//     progress_txt: function () {
//       this.rotate1 = 180;
//       this.rotate2 = 180;
//       this.draw();
//     },
//   },
  methods: {
    // draw() {
    //   let step = 360 / 100; 
    //   let progress = (180 / this.time/2.5) * (500 / 1000);
    //   if (this.progress_txt > 50) {
    //     let maxRotate = (this.progress_txt - 50) * step + 180;
    //     this.progress_txt = 0
    //   let rotate1Inter = setInterval(() => {
    //       this.rotate1 = this.rotate1 + progress;
    //       this.progress_txt += 1
    //       if (this.rotate1 >= 360) {
    //         this.rotate1 = 0;
    //         clearInterval(rotate1Inter);
    //         let rotate2Inter = setInterval(() => {
    //         this.progress_txt!=100?this.progress_txt += 1:''
    //           this.rotate2 = this.rotate2 + progress;
    //           if (this.rotate2 >= maxRotate) {
    //             clearInterval(rotate2Inter);
    //           }
    //         }, 100);
    //       }
    //     }, 100);
    //   }
    // },

     draw() {
      let step = 360 / 100; 
      let progress = (180 / this.time/2.5) * (500 / 1000)*-1;
      if (this.progress_txt > 50) {
        this.progress_txt = 0
      let rotate1Inter = setInterval(() => {
          this.rotate2 = this.rotate2 + progress;
          this.progress_txt += 1
          if (this.rotate2 <=0) {
            this.rotate2 = 0;
            clearInterval(rotate1Inter);
            let rotate2Inter = setInterval(() => {
            this.progress_txt!=100?this.progress_txt += 1:''
              this.rotate1 = this.rotate1 + progress;
              if (this.rotate1 <= 0) {
                this.rotate1 = 0
                clearInterval(rotate2Inter);
              }
            }, 100);
          }
        }, 100);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.progress_box {
  display: flex;
  justify-content: center;
  align-items: center;

  .inner_box {
    height: 300px;
    width: 300px;
    position: relative;
    overflow: hidden;
    border-radius: 50%;
    .position_view {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translateX(-50%) translateY(-50%);
    }

    .progress_circle {
      position: absolute;
      height: 300px;
      width: 300px;
      border-radius: 50%;
      z-index: 1000;
      overflow: hidden;
      display: flex;

      // background: #5AA2FC;
      .p_left {
        width: 150px;
        height: 300px;
        position: relative;
        overflow: hidden;
        background: linear-gradient(to left, #00f2fe, #4facfe);

        .left_mask {
          // top right bottom left
          position: absolute;
          top: 0;
          left: 0px;
          width: 300px;
          height: 300px;
          border-radius: 50%;
          clip: rect(0px, 300px, 300px, 150px);
          background: rgb(230, 227, 232);
        }
      }

      .p_right {
        width: 150px;
        height: 300px;
        background: linear-gradient(to right, #00f2fe, #4facfe);
        position: relative;
        overflow: hidden;

        .right_mask {
          position: absolute;
          top: 0;
          left: -150px;
          width: 300px;
          height: 300px;
          border-radius: 50%;
          clip: rect(0px, 150px, 300px, 0px);
          background: rgb(230, 227, 232);
        }
      }
    }

    .mask_circle {
      height: 254px;
      width: 254px;
      background: rgb(255, 255, 255);
      border-radius: 50%;
      z-index: 1001;
    }

    .progress_txt {
      position: absolute;
      top: 0;
      left: 0;
      width: 300px;
      height: 300px;
      font-size: 28px;
      color: #999999;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
    }

    .progress_info {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 52px;
      color: #333333;
      font-size: 36px;
    }

    .txt {
      text-align: center;
      font-size: 76px !important;
      font-weight: 500;
    }
  }
}

.yuanpan {
  margin: 0;
  padding: 0;
  height: 300px;
  height: 300px;
  // position: relative;
  position: absolute;
  left: -6px;
}

.yuanpan .kedu {
  width: 10px;
  height: 30px;
  background: white;
  position: absolute;
  left: 150px;
  top: 0;
  -webkit-transform-origin: center 152px;
  z-index: 99999;
}
</style>