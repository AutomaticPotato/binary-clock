<script lang="ts" setup>
import { computed } from 'vue';

const props = defineProps<{
    active: boolean
    binaryRow: number
}>()

const background = computed(() => ({
    "bg-red-600 scale-110": props.active,
    "bg-slate-400 scale-100": !props.active
}))
</script>

<template>
    <div :class="background"
        class="size-20 transition-all duration-500 rounded-md drop-shadow-md flex justify-center items-center text-white">
        <span v-if="active">{{ binaryRow }}</span>
    </div>
</template>