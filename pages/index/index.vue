<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<view class="uni-flex uni-column" style="margin-top: 24px;">
			<button type="default" @click="handleSignTextClient">
				签名输出
			</button>
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
				title: 'Hello, World'
			}
		},
		onLoad() {

		},
		methods: {
			handleSignTextClient: function(e){
				// #ifdef APP-ANDROID
				const result = signer.signToHex('ab', Math.floor(new Date().getTime() / 1000));
				if (!result || result.code != undefined) {
					console.log('error: '+ result.msg);
					return;
				}
				const {data} = result;
				console.log('signed: ' + data);
				// #endif
				
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
