<template>
	<div class="m-5">
		<div class="px-2 pb-2" id="qrcode">
			<div
				v-if="variant === 'Square'"
				:style="backgroundStyle"
				class="rounded custom-shadow p-5"
			>
				<slot />
			</div>
			<div
				v-else-if="variant === 'Hexagon'"
				:style="backgroundStyle"
				class="hexagon custom-shadow"
			>
				<slot />
			</div>
			<div
				v-else-if="variant === 'Circle'"
				:style="backgroundStyle"
				class="circle custom-shadow p-10"
			>
				<slot />
			</div>
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
	-webkit-box-shadow: 0px 5px 8px -1px rgba(0,0,0,0.5);
	box-shadow: 0px 5px 8px -1px rgba(0,0,0,0.5);
	background-color: white;
}
</style>