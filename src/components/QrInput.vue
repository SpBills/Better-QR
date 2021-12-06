<template>
    <div class="flex">
        <div>
            <input placeholder="Put your data here." v-model="qrcodeValue" @input="generate()" class="border-b-2 mr-3" />
        </div>
        <div class="radios pr-5 w-24">
            <div v-for="label in radioValues" :key="label" class="flex items-center">
                <label :for="label">{{ label }}</label>
                <input class="ml-auto" type="radio" v-model="picked" :id="label" :value="label" @input="generate()"/>
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
    emits: ["generate"],
    setup(props, context) {
        const qrcodeValue = ref("");
        const radioValues = ["Square", "Circle"];
        const picked = ref("");
        const colors = ref("#000");

        const generate = () => {
            context.emit("generate", {
                qr: qrcodeValue.value,
                variant: picked.value,
                colors: colors.value,
            });
        };

        return {
            qrcodeValue,
            generate,
            radioValues,
            picked,
            colors,
        };
    },
};
</script>

<style>
h1 {
    font-family: raleway;
}
</style>