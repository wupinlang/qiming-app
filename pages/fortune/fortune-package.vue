<template>
	<view class="body">
		<image class="banner" mode="widthFix" src="../../static/banner2.png"></image>

		<view class="packages">
			<view @click="handleSelect(item)" v-for="(item, index) in packages" :class="['package', selectedPackage && selectedPackage.id === item.id ? 'selected' : 'unselected']">
				<view>
					<view class="price">
						<view class="discount">特惠价：{{ item.discountedPrice }}</view>
						<view class="regular">原价：{{ item.regularPrice }}</view>
					</view>
					<view class="desc">{{ item.name }}：{{ item.description }}</view>
				</view>
			</view>
		</view>

		<image class="divider" mode="widthFix" src="../../static/divider.png"></image>

		<view class="pay" v-if="selectedPackage">
			<view class="title">请选择支付方式</view>
			<view class="subtitle">
				支付金额：
				<text class="price">{{ selectedPackage.discountedPrice }}元</text>
			</view>

			<view class="pay-btn wx" @click="() => payWith('WeChat', selectedPackage.discountedPrice)">
				<image src="../../static/wx.png"></image>
				点此微信支付
			</view>
			<view class="pay-btn zfb" @click="() => payWith('Taobao', selectedPackage.discountedPrice)">
				<image src="../../static/zfb.png"></image>
				点此支付宝支付
			</view>
		</view>

		<view class="notice">
			<image mode="widthFix" src="../../static/notice.png"></image>
			<view>支付系统经过安全联盟和可信网站认证，请放心使用</view>
		</view>

		<div v-html="paymentForm" />
	</view>
</template>

<script>
export default {
	data() {
		return {
			packages: [],
			selectedPackage: null,

			paymentForm: ''
		};
	},
	onLoad(option) {
		this.fetchPackages(option.orderId);
	},
	methods: {
		async fetchPackages(orderId) {
			uni.showLoading({
				mask: true
			});
			const result = await uni.request({
				url: '/package_option/fortune_service',
				data: {
					orderId
				}
			});
			uni.hideLoading();
			// this.packages=[{
			// 	id: 1,
			// 	discountedPrice: '11',
			// 	regularPrice: '22',
			// 	name: '33',
			// 	description: '55'
			// },{
			// 	id: 2,
			// 	discountedPrice: '11',
			// 	regularPrice: '22',
			// 	name: '套餐2',
			// 	description: '55'
			// }]
			// this.selectedPackage = {
			// 	id: 1,
			// 	discountedPrice: '11',
			// 	regularPrice: '22',
			// 	name: '33',
			// 	description: '55'
			// }
			this.packages = result.data;
			this.selectedPackage = result.data[0];
		},
		handleSelect(pack) {
			this.selectedPackage = pack;
		},
		async payWith(method, amount) {
			const { orderId } = this.options;

			const data = {
				orderId: Number(orderId),
				method,
				amount
			};

			const res = await uni.request({
				url: '/payment',
				method: 'POST',
				data
			});

			const json = res.data;

			this.paymentForm = json.form;
			this.$nextTick(() => {
				document.forms['punchout_form'].submit();
			});
		}
	}
};
</script>

<style lang="scss" scoped>
.body {
	background-color: #eeeeee;
	min-height: 100vh;
}

.banner {
	width: 100vw;
}

.packages {
	width: 100%;
	display: flex;
	flex-direction: column;
	align-items: center;

	.package {
		width: 650rpx;
		display: flex;
		align-items: center;
		margin-top: 25rpx;
		border-width: 1px;
		border-color: rgb(210, 210, 210);
		border-style: solid;
		border-radius: 10rpx;

		height: 150rpx;
		padding: 0 25rpx;

		.price {
			display: flex;
			.discount {
				font-size: 36rpx;
				font-family: 'PingFang';
				color: rgb(218, 41, 44);
				font-weight: bold;
			}
			.regular {
				font-size: 24rpx;
				font-family: 'PingFang';
				color: rgba(87, 87, 87, 0.671);
				font-weight: bold;
				text-decoration: line-through;
				line-height: 2.5;
				margin-left: 10rpx;
			}
		}
		.desc {
			font-size: 26rpx;
			font-family: 'PingFang';
			color: rgb(36, 36, 36);
			font-weight: bold;
		}
	}
}

.selected {
	background-image: -moz-linear-gradient(90deg, rgb(252, 234, 172) 0%, rgb(254, 245, 210) 100%);
	background-image: -webkit-linear-gradient(90deg, rgb(252, 234, 172) 0%, rgb(254, 245, 210) 100%);
	background-image: -ms-linear-gradient(90deg, rgb(252, 234, 172) 0%, rgb(254, 245, 210) 100%);
}
.unselected {
	background-color: #ffffff;
}
.divider {
	width: 700rpx;
	margin-left: 25rpx;
	margin-top: 30rpx;
}
.pay {
	padding: 25rpx 35rpx;
	color: rgb(88, 88, 88);
	font-size: 24rpx;
	font-weight: bold;

	.title {
		font-size: 36rpx;
		font-family: 'PingFang';
		color: rgb(36, 36, 36);
	}

	.subtitle {
		margin: 8rpx;
		margin-bottom: 16rpx;
	}
	.price {
		font-size: 36rpx;
		font-family: 'PingFang';
		color: rgb(218, 41, 44);
		font-weight: bold;
	}
	.pay-btn {
		font-size: 36rpx;
		font-family: 'PingFang';
		color: rgb(255, 255, 255);
		border-radius: 10px;
		width: 444rpx;
		height: 96rpx;
		display: flex;
		align-items: center;
		padding-left: 100rpx;
		margin-bottom: 30rpx;
	}

	.wx {
		background-color: rgb(50, 181, 90);
		image {
			width: 62rpx;
			height: 62rpx;
			margin-left: 10rpx;
			margin-right: 10rpx;
		}
	}
	.zfb {
		background-color: rgb(0, 169, 242);
		image {
			width: 72rpx;
			height: 72rpx;
			margin-right: 10rpx;
		}
	}
}
.notice {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	margin-top: 100rpx;
	// position: absolute;
	// width: 100vw;
	// bottom: 10rpx;

	view {
		font-size: 20rpx;
		font-family: 'PingFang';
		color: rgb(25, 170, 15);
		font-weight: bold;
		margin-top: 10rpx;
	}
}
</style>
