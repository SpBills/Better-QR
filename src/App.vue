<template>
    <div class="h-screen flex justify-center items-center">
        <div class="shadow p-5 flex flex-col">
            <h1 class="text-3xl font-extrabold">Pretty QRCode Generator</h1>
            <qr-code
                :value="qrcodeValue"
                :variant="variant"
                :background="color"
            />
            <qr-input @generate="generate" />
            <qr-save class="mt-5" />
        </div>
    </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import QrCode from "./components/QrCode.vue";
import QrInput from "./components/QrInput.vue";
import QrSave from "./components/QrSave.vue";

export default {
    components: {
        QrCode,
        QrInput,
        QrSave,
    },
    setup() {
        const qrcodeValue = ref("");
        const variant = ref("Square");
        const color = ref("#3872ba");
        const generate = (val) => {
            qrcodeValue.value = val.qr;
            variant.value = val.variant;
            color.value = val.colors;
        };

        return {
            generate,
            qrcodeValue,
            variant,
            color,
        };
    },
    name: "App",
};
</script>

<style>
</style>
