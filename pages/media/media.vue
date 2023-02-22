<template>
	<view>
		<button @click="chooseImage">chooseImage</button>
		<button @click="chooseImagePreview">chooseImagePreview</button>
		<button @click="previewImage">previewImage</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
tempFilePaths:[]
			}
		},
		methods: {
			/**
			 * 这个方法会调用系统的选择器，好不好用取决于系统。例如小米就很好用，预览编辑功能都是能直接用的。
			 * 在PC上是很简单的，看不出具体功能。
			 */
			chooseImage() {
				uni.chooseImage({
					count: 6, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: function(res) {
						console.log(JSON.stringify(res.tempFilePaths));
						this.tempFilePaths=res.tempFilePaths
						console.log(this.tempFilePaths);
						uni.saveFile({
							tempFilePaths:this.tempFilePaths
						})
					}
				});
			},
			chooseImagePreview() {
				// 从相册选择6张图
				uni.chooseImage({
					count: 6,
					sizeType: ['original', 'compressed'],
					sourceType: ['album'],
					success: function(res) {
						// 预览图片,这个方法真机上实际上是没什么用的。因为默认就有预览功能
						uni.previewImage({
							urls: res.tempFilePaths,
							longPressActions: {
								itemList: ['发送给朋友', '保存图片', '收藏'],
								success: function(data) {
									console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data
										.index + 1) + '张图片');
								},
								fail: function(err) {
									console.log(err.errMsg);
								}
							}
						});
					}
				});
			}
		},
		previewImage(){
			// 预览图片
			uni.previewImage({
				urls: this.tempFilePaths,
				longPressActions: {
					itemList: ['发送给朋友'],
					success: function(data) {
						console.log('选中了第' + (data.tapIndex + 1) + '个按钮,第' + (data
							.index + 1) + '张图片');
					},
					fail: function(err) {
						console.log(err.errMsg);
					}
				}
			});
		}
	}
</script>

<style scoped>

</style>
