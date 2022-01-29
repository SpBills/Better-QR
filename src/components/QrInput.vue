<template>
    <div>
        <div class="flex flex-col">
            <div class="mb-5">
                <label>Size</label>
                <vue-slider :color="colors" :min="10" :max="300" v-model="size" />
            </div>
            <div>
            <div>
                <input
                    placeholder="Link Goes here"
                    v-model="qrcodeValue"
                    @input="generate()"
                    class="border-b-2 mr-3"
                />
            </div>
            <div class="radios pr-5 w-24">
                <div
                    v-for="label in radioValues"
                    :key="label"
                    class="flex items-center"
                >
                    <label :for="label">{{ label }}</label>
                    <input
                        class="ml-auto"
                        type="radio"
                        v-model="picked"
                        :id="label"
                        :value="label"
                        @click="sendUpRadio"
                    />
                </div>
            </div>
            </div>
        </div>
        <h3>Background Color</h3>
        <div class="shadow-xl w-1/3">
            <color-picker disableHistory disableAlpha v-model:pureColor="colors" />
        </div>
    </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { watch } from "@vue/runtime-core";

import VueSlider from 'vue-slider-component'
import 'vue-slider-component/theme/antd.css'

export default {
    components: {
        VueSlider,
    },
    emits: ["generate"],
    setup(props, context) {
        const qrcodeValue = ref("");
        const radioValues = ["Square", "Circle"];
        const picked = ref("Square");
        const size = ref(150);
        const colors = ref("#3872ba");

        watch(
            () => [colors.value, size.value],
            ([color, sz], [_prevColor, _prevSize]) => {
                context.emit("generate", {
                    qr: qrcodeValue.value,
                    variant: picked.value,
                    size: sz,
                    colors: color,
                });
            }
        );

        const generate = () => {
            context.emit("generate", {
                qr: qrcodeValue.value,
                variant: picked.value,
                size: size.value,
                colors: colors.value,
            });
        };

        const sendUpRadio = (evt) => {
            context.emit("generate", {
                qr: qrcodeValue.value,
                variant: evt.target.value,
                size: size.value,
                colors: colors.value,
            });
        };

        return {
            qrcodeValue,
            generate,
            radioValues,
            picked,
            colors,
            sendUpRadio,
            size
        };
    },
};
</script>

<style>
h1 {
    font-family: raleway;
}

.vc-color-wrap {
    width: 100% !important;
}
</style>