<template>
	<button type="button" :class="classes" @click="onClick" :style="style">
		{{ label }}
	</button>
</template>

<script>
export default {
	name: 'app-button',
	props: {
		label: {
			type: String,
			required: true,
		},
		primary: {
			type: Boolean,
			default: false,
		},
		disabled: {
			type: Boolean,
			default: false,
		},
		size: {
			type: String,
			default: 'medium',
			validator: function (value) {
				return ['small', 'medium', 'large'].indexOf(value) !== -1;
			},
		},
		color: {
			type: String,
		},
	},
	computed: {
		classes() {
			return {
				button: true,
				'button--primary': this.primary,
				'button--secondary': !this.primary,
				'button--disabled': !this.primary && this.disabled,
				[`button--${this.size}`]: true,
			};
		},
		// Storybook을 위해 사용되는 computed value
		style() {
			if (this.disabled) return;
			return {
				backgroundColor: this.primary ? this.color : '#fff',
				borderColor: !this.primary ? this.color : '#fff',
				color: !this.primary ? this.color : '#fff',
			};
		},
	},

	methods: {
		onClick() {
			this.$emit('onClick');
		},
	},
};
</script>

<style lang="scss" scoped>
.button {
	// display: inline-block;
	border: 1px solid #4f00ff;
	border-radius: 4px;
	color: #4f00ff;
	font: {
		family: inherit;
		weight: 700;
	}
	letter-spacing: 0.16px;
	text-align: center;
	cursor: pointer;

	// enabled, disabled, un-fill
	&--primary {
		color: white;
		background-color: #4f00ff;
	}
	&--secondary {
		background-color: #fff;
	}
	&--disabled {
		cursor: not-allowed;
		color: #999;
		background-color: #f3f3f3;
		border: 1px solid #eaeaea;
	}
	// 각 button의 width 값은 변경될 수 있음
	&--small {
		font-size: 14px;
		padding: 10px 16px;
		width: 288px;
	}
	&--medium {
		padding: 11px 20px;
		font-size: 16px;
		width: 320px;
	}
	&--large {
		font-size: 16px;
		padding: 15px 24px;
		width: 392px;
	}
}

// 버튼의 높이를 표현해야 하는 경우가 생긴다면
.btn {
	&.h-lg {
		height: 3.5rem;
		line-height: 3.5rem;
	}
}
</style>