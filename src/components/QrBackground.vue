<template>
	<div class="custom-shadow m-5 rounded flex">
		<div
			v-if="variant === 'Square'"
			:style="backgroundStyle"
			class="rounded p-5 inline-block"
			id="qrcode"
		>
			<slot />
		</div>
		<div
			v-else-if="variant === 'Hexagon'"
			:style="backgroundStyle"
			class="hexagon shadow"
			id="qrcode"
		>
			<slot />
		</div>
		<div
			v-else-if="variant === 'Circle'"
			:style="backgroundStyle"
			class="circle p-10 shadow inline-block"
			id="qrcode"
		>
			<slot />
		</div>
	</div>
</template>

<script>
export default {
	props: {
		variant: {
			type: String,
			required: true,
		},
		background: {
			type: String,
			required: true,
		},
	},
	data() {
		return {
			backgroundStyle: {
				backgroundColor: this.background,
			},
		};
	},
	methods: {},
	watch: {
		background: function (back, prevBack) {
			this.backgroundStyle = {
				backgroundColor: back,
			};
		},
	},
};
</script>

<style>
.circle {
	border-radius: 100%;
}
.custom-shadow {
	-webkit-box-shadow: 0px 5px 8px -1px #b0b0b0;
	box-shadow: 0px 5px 8px -1px #b0b0b0;
}
</style>