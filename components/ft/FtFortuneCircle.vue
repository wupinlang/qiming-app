<template>
	<view class="ft-fortune-container">
		<view class="ft-fortune-circle">
			<view class="ft-fortune-circle-background-outer" />
			<view class="ft-fortune-circle-background-inner" />
			<view class="ft-fortune-circle-outer">
				<span v-for="(text, i) in outerText" :style="rotate(i)">{{ text }}</span>
			</view>
			<view class="ft-fortune-circle-inner">
				<span v-for="(text, i) in innerText" :style="rotate(i)">{{ text }}</span>
			</view>
			<view class="ft-fortune-circle-base" />
		</view>
	</view>
</template>

<script setup>
const innerText = '甲己-中正土  乙庚-仁义金  丙辛-威制水  丁壬-淫慝木  戊癸-无情火';
const outerText = '三会    亥子丑:水   寅卯辰:木   巳午未:火   申酉戌:金';

const rotate = (i) => {
	return `transform: rotate(${9 * i}deg)`;
};
</script>

<style>
.ft-fortune-container {
	display: grid;
	place-content: center;
}

.ft-fortune-circle {
	position: relative;
	width: 600rpx;
	height: 600rpx;
	display: flex;
	justify-content: center;
	align-items: center;
}

.ft-fortune-circle-base {
	position: absolute;
	width: 380rpx;
	height: 380rpx;
	margin: 0 auto;

	background-image: url('../../static/fortune-circle.png');
	background-size: cover;
	background-repeat: no-repeat;
}

.ft-fortune-circle-background-inner {
	height: 500rpx;
	width: 500rpx;
	position: absolute;
	background-color: #cea660;
	border-radius: 50%;
}

.ft-fortune-circle-background-outer {
	height: 100%;
	width: 100%;
	position: absolute;
	background-color: #935e35;
	border-radius: 50%;
}

.ft-fortune-circle-inner {
	height: 100%;
	width: 100%;
	position: absolute;
	color: #4a272a;
}

.ft-fortune-circle-outer {
	height: 100%;
	width: 100%;
	position: absolute;
	color: #ffe1b5;
}

.ft-fortune-circle-inner span {
	position: absolute;
	font-size: 30rpx;
	top: 70rpx;
	left: 50%;
	transform-origin: 0 230rpx;
}

.ft-fortune-circle-outer span {
	position: absolute;
	font-size: 22rpx;
	top: 10rpx;
	left: 50%;
	transform-origin: 0 290rpx;
}
</style>
