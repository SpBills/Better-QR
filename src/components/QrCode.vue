<template>
    <div class="inline-block bg-transparent" id="qrcode">
        <qr-background :variant="variant">
            <qrcode-vue :value="value" :background="background" />
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
    props: {
        value: {
            type: String,
            required: true,
        },
        variant: {
            type: String,
            required: false,
        },
        background: {
            type: String,
            required: false,
            default: "#fff"
        }
    },
    setup() {},
};
</script>

<style>
</style>