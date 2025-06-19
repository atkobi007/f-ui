<template>
	<view class="uni-margin-wrap">
		<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
			:duration="duration">
			<swiper-item>
				<view class="swiper-item uni-bg-red">A</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-green">B</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-blue">C</view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script setup>
	import {
		ref
	} from "vue"
	const background = ref(['color1', 'color2', 'color3']);
	const indicatorDots = ref(true);
	const autoplay = ref(true);
	const interval = ref(2000);
	const duration = ref(500)
	console.error("vue")
	const changeIndicatorDots = (e) => {
		indicatorDots.value = !indicatorDots.value
	}
	const changeAutoplay = (e) => {
		autoplay.value = !autoplay.value
	}
	const intervalChange = (e) => {
		interval.value = e.target.value
	}
	const durationChange = (e) => {
		duration.value = e.target.value
	}
</script>

<style lang="scss" scoped>
	.uni-margin-wrap {
		width: 690rpx;
		width: 100%;
	}

	.swiper {
		width: 100%;
		height: 300rpx;
	}

	.swiper-item {
		display: flex;
		height: 320rpx;
	}

	.swiper-list {
		margin-top: 40rpx;
		margin-bottom: 0;
	}

	.uni-common-mt {
		margin-top: 60rpx;
		position: relative;
	}

	.info {
		position: absolute;
		right: 20rpx;
	}

	.uni-padding-wrap {
		width: 550rpx;
		padding: 0 100rpx;
	}

	.uni-bg-red {
		background: red;
	}

	.uni-bg-green {
		background: green;
	}

	.uni-bg-blue {
		background: blue;
	}
</style>