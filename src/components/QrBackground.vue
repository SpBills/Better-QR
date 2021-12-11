<template>
    <div
        v-if="!variant"
        :style="background"
        class="p-5 m-5 rounded inline-block"
        id="qrcode"
    >
        <slot />
    </div>
    <div
        v-else-if="variant === 'Square'"
        :style="backgroundStyle"
        class="p-5 m-5 rounded inline-block custom-shadow"
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
        class="circle p-10 m-5 shadow inline-block"
        id="qrcode"
    >
        <slot />
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