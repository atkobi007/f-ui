<template name="fui-button">
	<view class="fui-button" :style="getBackGroundColor" @touchstart="onTouchStart" @touchcancel="onTouchEnd"
		@touchend="onTouchEnd">
		<view class="button-container">
			<slot name="icon" v-if="iconPositon=='LEFT'"></slot>
			<view class="button-text-container">
				<slot name="icon" v-if="iconPositon=='TOP'"></slot>
				<text :style="getTextColor">{{text}}</text>
				<slot name="icon" v-if="iconPositon=='BOTTOM'"></slot>
			</view>
			<slot name="icon" v-if="iconPositon=='RIGHT'"></slot>
		</view>
	</view>
</template>

<script setup>
	import {
		ref,
		onMounted,
		computed		
	} from "vue";

	const props = defineProps({
		//是否按下后按钮变化
		downAnimation: {
			type: Boolean,
			default: true
		},
		//默认文字颜色
		textColor: {
			type: String,
			default: "#000"
		},
		//按下后文字颜色
		downTextColor: {
			type: String,
			default: ""
		},
		//默认背景颜色,border 背景色，
		//可设置渐变 linear-gradient(to right,red,blue)
		//注意:设置 plain: true后不可设置为渐变色背景,否则border 不生效
		backGroundColor: {
			type: String,
			default: "gray"
		},
		//按下后背景颜色
		downBackGroundColor: {
			type: String,
			default: ""
		},
		//是否禁用
		disabled: {
			type: Boolean,
			default: false
		},
		//文字内容
		text: {
			type: String,
			default: "BUTTON"
		},
		//ICON 位置
		iconPositon: {
			type: String,
			default: "LEFT"
		},
		//设置圆角按钮 "square" | "circle",
		shape: {
			type: String,
			default: "square"
		},
		//是否缕空
		plain: {
			type: Boolean,
			default: false,
		}
	})

	/** 
	 * 按钮状态 0:默认 1:按下  2:禁用
	 */
	const buttonState = ref(0)

	onMounted(() => {
		buttonState.value = props.disabled ? 2: 0;
	})

	const onTouchStart = () => {
		if (props.disabled || !props.downAnimation) return;
		buttonState.value = 1
	}
	const onTouchEnd = () => {
		if (props.disabled || !props.downAnimation) return;
		buttonState.value = 0
	}
	//长按弹窗检查信息
	const onContextMenu = (e) => {
		e.preventDefault();
	}

	/**
	 * 设置文字颜色
	 **/
	const getTextColor = computed(() => {
		const pos = props.iconPositon
		const color = props.disabled ? "#666" : buttonState.value == 1 ?
				props.downTextColor.length>0?props.downTextColor:props.textColor : props.textColor
		return {
			color: color,
			"margin-left": pos == "LEFT" ? "8rpx" : "0px",
			"margin-right": pos == "RIGHT" ? "8rpx" : "0px",
			"margin-top": pos == "TOP" ? "8rpx" : "0px",
			"margin-bottom": pos == "BOTTOM" ? "8rpx" : "0px",
		}
	})
	/**
	 * 设置背景颜色
	 **/
	const getBackGroundColor = computed(() => {
		const shape = props.shape;
		let shapeValue = shape == "circle" ? "100rpx" : "6rpx";
		const defaultColor = props.backGroundColor;
		const downBgColor = props.downBackGroundColor;
		let bgColor = props.disabled ? "#ccc" : buttonState.value == 1 ?
			downBgColor.length > 0 ? downBgColor : defaultColor : defaultColor;
		const borderColor = `1px solid ${bgColor}`;
		if (props.plain) {
			bgColor = "transparent";
		}
		return {
			"background": bgColor,
			"border-radius": shapeValue,
			"border": borderColor,
		}
	});
</script>

<style lang="scss" scoped>
	.fui-button {
		border-radius: 6rpx;
		padding: 10rpx 20rpx;
		margin: 0px auto;
	}

	.button-container {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
	}

	.button-text-container {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>