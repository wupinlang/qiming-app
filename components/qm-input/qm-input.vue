<template>
	<view>
		<input placeholder-class="placeholder" @input="handleInput" :style="`width: ${width}rpx`" :placeholder="placeholder" class="qm-input"/>
	</view>
</template>

<script>
	export default {
		name:"qm-input",
		props: ['modelValue', 'width', 'placeholder'],
		emits: ['update:modelValue'],
		data() {
			return {
				
			};
		},
		methods: {
			handleInput(e) {
				console.log(e, e.detail.value)
				this.$emit('update:modelValue', e.detail.value)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.qm-input {
	  border: 1px solid rgb(215, 51, 64);
	  border-radius: 10rpx;
	  height: 60rpx;
	  padding: 0 20rpx;
	  font-size: 30rpx;
	}
	.placeholder {
		color: #b8b8b8;
	}
</style>