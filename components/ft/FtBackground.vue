<template>
	<view class="ft-background">
		<slot />
	</view>
</template>

<script></script>

<style scoped>
.ft-background {
	padding-top: 100rpx;
	box-sizing: border-box;
	min-height: 100vh;
	background-color: #ea3f4a;
	background-image: url('../../static/ft-background.png');
	background-repeat: no-repeat;
	background-size: contain;
}
</style>
