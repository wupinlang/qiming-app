<template>
	<view class="ft-homepage">
		<view class="ft-homepage-label-input-form">
			<FtHomepageLabel type="name" v-model="name" />
			<FtHomepageLabel type="gender" v-model="gender" />
			<FtHomepageLabel type="birthdate" v-model="birthdate" />
		</view>
		<view class="ft-start-button" @click="handleSubmit" />
		<view class="ft-homepage-master-qr" />
	</view>
</template>

<script setup>
import { ref } from 'vue';
import FtHomepageLabel from '../../components/ft/FtHomepageLabel.vue';

const name = ref('');
const gender = ref('男');
const birthdate = ref('');

const handleSubmit = () => {
	uni.navigateTo({
		url: `/pages/fortune/fortune-payment`
	});
};
</script>

<style scoped>
.ft-homepage {
	width: 750rpx;
	height: 4659rpx;
	background-image: url('../../static/ft-homepage.png');
	background-repeat: no-repeat;
	background-size: contain;
}

.ft-homepage-label-input-form {
	position: absolute;
	top: 710rpx;
	left: 50%;
	transform: translateX(-50%);
	display: grid;
	gap: 45rpx;
}

.ft-start-button {
	position: absolute;
	top: 1150rpx;
	left: 50%;
	width: 700rpx;
	height: 120rpx;
	background-image: url('../../static/ft-start-button.png');
	background-repeat: no-repeat;
	background-size: contain;
	animation: 0.8s ease-in-out infinite alternate breath;
}

@keyframes breath {
	from {
		transform: translateX(-50%) scale(1.05);
	}
	to {
		transform: translateX(-50%) scale(0.95);
	}
}

.ft-homepage-master-qr {
	position: absolute;
	top: 3790rpx;
	left: 140rpx;
	width: 500rpx;
	height: 500rpx;
	background-image: url('../../static/wechat-public-qrcode.jpg');
	background-repeat: no-repeat;
	background-size: contain;
}
</style>
