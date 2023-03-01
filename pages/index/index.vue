<template>
	<view>
		<view class="content">
			<image class="logo" src="/static/app_logo.png"></image>
			<view class="text-area" style="margin-bottom: 24px;">
				<text class="title" style="font-size: 24px; color: rgba(0, 0, 0, .85);">{{title}}</text>
			</view>
		</view>
		<view style="padding: 0 0 24px 0;">
			<view class="text-box" style="padding: 0 24px 8px 24px; text-align: center!important;">
				<text style="color: rgba(0, 0, 0, .45);">
					签名内容
				</text>
				<br/>
				<text style="word-wrap:break-word; word-break:break-all; color: rgba(0, 0, 0, .65); font-size: 18px;">
					{{msg}}
				</text>
			</view>
			<view class="text-box" style="padding: 0 24px 8px 24px; text-align: center!important;">
				<text style="color: rgba(0, 0, 0, .45);">
				签名结果
				</text>
				<br/>
				<text style="word-wrap:break-word; word-break:break-all; color: rgba(0, 0, 0, .65); font-size: 18px;">
					{{digest}}
				</text>
			</view>
		</view>
		<view class="uni-padding-wrap uni-common-mt" style="padding: 0 24px 8px 24px;">
			<button style="margin-bottom: 8px;" type="primary" @click="handleCopyBtnClick">复制签名摘要</button>
			<button style="margin-bottom: 8px;" type="default" @click="handleVerifyBtnClick">校验签名摘要</button>
		</view>
	</view>
	
</template>

<script>
	// #ifdef APP-ANDROID
	const signer = uni.requireNativePlugin("SignerModule");
	// #endif
	export default {
		data() {
			return {
				title: 'Hello, Signer',
				msg: 'a=1&b=2&c=3&d=4&e=5',
				digest: '',
			}
		},
		onLoad() {
			// #ifdef APP-ANDROID
			/**
			 * signToHex 签名方法导出十六进制签名摘要
			 * 参数 msg: 签名内容
			 * 返回: 结果对象; 若成功 result.data 字段为十六进制签名摘要
			 */
			const result = signer.signToHex(this.msg);
			if (!result || result.code != undefined) {
				console.log('签名失败: '+ result.msg);
				return;
			}
			const {data} = result;
			console.log(`签名摘要: ${data}`);
			this.digest = data;
			// #endif
		},
		methods: {
			handleCopyBtnClick(e){
				uni.setClipboardData({
					data: this.digest,
					success: function () {
						uni.showToast({
							title: '复制成功',
							icon: 'none',
							position: 'bottom',
						});
					}
				});
			},
			handleVerifyBtnClick(){
				uni.showToast({
					title: '暂不支持此功能',
					icon: 'none',
					position: 'bottom',
				});
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
