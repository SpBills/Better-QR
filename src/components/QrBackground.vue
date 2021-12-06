<template>
    <div v-if="!variant" class="p-5 m-5 shadow">
        <slot />
    </div>
    <div v-else-if="variant === 'Square'" class="bg rounded p-5 m-5 shadow">
        <slot />
    </div>
    <div v-else-if="variant === 'Hexagon'" class="hexagon bg shadow">
        <slot />
    </div>
    <div v-else-if="variant === 'Circle'" class="circle bg p-10 m-5 shadow">
        <slot />
    </div>
</template>

<script>
export default {
    props: {
        variant: {
            type: String,
            required: false,
        },
    },
};
</script>

<style>
.circle {
    border-radius: 100%;
}

.bg {
    background-color: white;
}
</style>