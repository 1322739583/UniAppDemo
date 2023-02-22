<template>
  <view>
    <button @click="vibrate">vibrate</button>
    <button @click="vibrateLong">vibrateLong</button>
    <button @click="vibrateShort">vibrateShort</button>
    <button @click="vibrateCustom">vibrateCustom(先短后长)</button>

  </view>
</template>

<script>
export default {
  data() {
    return {}
  },
  methods: {
    /**
     * iOS上只有长震动，没有短震动
     * iOS上需要手机设置“打开响铃时震动”或“静音时震动”，否则无法震动
     * vibrate只适用于钉钉小程序、支付宝小程序
     * 默认就是短振动(15)，不可以设置时间
     */
    vibrate() {
      uni.vibrate({
        success: function () {
          console.log('success');
        }
      });
    },
    /**
     * 振动400ms,非常的明显
     */
    vibrateLong() {
      uni.vibrateLong({
        success: function () {
          console.log('success');
        }
      });
    },
    vibrateShort() {
      uni.vibrateShort({
        success: function () {
          console.log('success');
        }
      });
    },
    vibrateCustom() {
      //这样写是能保证同步的
      new Promise((resolve, reject) => {
        //共600ms
        let count1 = 0;
        const id1 = setInterval(() => {
          if (count1 >= 100) {
            clearInterval(id1)
            resolve()
          }
          uni.vibrateShort()
          count1++
          console.log("count1:",count1)
        }, 15)

      }).then(()=>{
        let count2=0;
        const id2 = setInterval(() => {
          if (count2 >= 5) clearInterval(id2)
          uni.vibrateLong()
          count2++
          console.log("count2:",count2)
        }, 400)
      })


    }
  }
}
</script>

<style scoped>

</style>