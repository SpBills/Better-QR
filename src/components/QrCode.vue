<template>
	<div class="flex justify-center bg-transparent">
		<qr-background :variant="variant" :background="background">
			<qrcode-vue
				:size="size"
				:value="value"
				:background="background"
				:foreground="foreground"
			/>
		</qr-background>
	</div>
</template>

<script>
import QrcodeVue from "qrcode.vue";
import QrBackground from "./QrBackground.vue";

export default {
	components: {
		QrcodeVue,
		QrBackground,
	},
	data() {
		return {
			foreground: "#000000",
		};
	},
	props: {
		value: {
			type: String,
			required: true,
		},
		variant: {
			type: String,
			required: true,
		},
		background: {
			type: String,
			required: false,
			default: "#3872ba",
		},
		size: {
			type: Number,
			required: false,
			default: 150
		}
	},
	created() {
		let backgroundHex = this.rgbToHex(this.background);

		this.foreground = this.pickTextColorBasedOnBgColorSimple(
			backgroundHex,
			"#FFFFFF",
			"#000000"
		);
	},
	methods: {
		rgbToHex(rgb) {
			return (
				"#" +
				rgb
					.slice(4, -1)
					.split(",")
					.map((x) => (+x).toString(16).padStart(2, 0))
					.join("")
			);
		},
		pickTextColorBasedOnBgColorSimple(bgColor, lightColor, darkColor) {
			var color =
				bgColor.charAt(0) === "#" ? bgColor.substring(1, 7) : bgColor;
			var r = parseInt(color.substring(0, 2), 16); // hexToR
			var g = parseInt(color.substring(2, 4), 16); // hexToG
			var b = parseInt(color.substring(4, 6), 16); // hexToB
			return r * 0.299 + g * 0.587 + b * 0.114 > 186
				? darkColor
				: lightColor;
		},
	},
	watch: {
		background: function (back, prevBack) {
			let backgroundHex = this.rgbToHex(back);

			this.foreground = this.pickTextColorBasedOnBgColorSimple(
				backgroundHex,
				"#FFFFFF",
				"#000000"
			);
		},
	},
	setup() {},
};
</script>

<style>
</style>