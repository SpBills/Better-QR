<template>
    <button class="px-5 py-3 bg-blue-400 text-white rounded" @click="download">
        SAVE
    </button>
</template>

<script>
import html2canvas from "html2canvas";

export default {
    setup() {
        const save = async () => {
            let canvas = await html2canvas(document.querySelector("#qrcode"), {
                backgroundColor: null,
            });

            return canvas.toDataURL();
        };

        const download = async () => {
            let b64 = await save();
            const name = "qrcodesave.png";

            let fetchedData = await fetch(b64);
            let blob = await fetchedData.blob();
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = name;
            link.click();
            URL.revokeObjectURL(link.href);
        };

        const copy = async () => {};

        return {
            save,
            download,
            copy,
        };
    },
};
</script>

<style>
</style>