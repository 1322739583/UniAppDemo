<template>
	<view>
		<button @click="getSystemInfo">getSystemInfo</button>
		<button @click="getDeviceInfo">getDeviceInfo</button>
		<button @click="getWindowInfo">getWindowInfo</button>
		<button @click="getAppBaseInfo">getAppBaseInfo</button>
		<button @click="getAppAuthorizeSetting">getAppAuthorizeSetting</button>
		<button @click="getSystemSetting">getSystemSetting</button>
		<button @click="openAppAuthorizeSetting">openAppAuthorizeSetting</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			getSystemInfo() {
				/**
				 * 返回到非常多的参数，大概有50个，你觉得应该有的都能看到。
				 */
        uni.getSystemInfo({
          success: function (res) {
            console.log("getSystemInfo:", res)
          }
        });
			},
			/**
			 * 需要写成直接返回对象而不是传对象的形式。不按套路出牌了。传对象是没有效果的。
			 * 就13个属性，大部分都可以在SystemInfo中获取到。
			 */
			getDeviceInfo() {
        const deviceInfo = uni.getDeviceInfo();
        console.log("deviceInfo:", deviceInfo);
			},
      /**
       * 十几个属性，都是从getSystemInfo里面扣出来的
       */
			getWindowInfo() {
        const windowInfo = uni.getWindowInfo();
        console.log("windowInfo:", windowInfo);
			},
      /**
       * appid,name,version,host
       */
			getAppBaseInfo() {
        const appBaseInfo = uni.getAppBaseInfo();
        console.log("appBaseInfo:", appBaseInfo);
			},
      /**
       * 能获取10几个权限的信息，相册，蓝牙，定位，手机号，通知，电话记录等
       */
      getAppAuthorizeSetting(){
        const getAppAuthorizeSetting = uni.getAppAuthorizeSetting();
        console.log("getAppAuthorizeSetting:", getAppAuthorizeSetting);
      },
      /**
       * 获取系统设置，例如蓝牙，屏幕方向，定位，wifi是否打开。内容很少，就这几个。
       */
      getSystemSetting(){
        const getSystemSetting = uni.getSystemSetting();
        console.log("getSystemSetting:", getSystemSetting);
      },
      /**
       * 会跳转到微信的应用信息界面
       */
      openAppAuthorizeSetting(){
        uni.openAppAuthorizeSetting({
          success (res) {
            //也就返回ok这样的简单信息
            console.log("openAppAuthorizeSetting:",res)
          }
        })
      }
		}
	}
</script>

<style scoped>

</style>
