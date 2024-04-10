<script setup lang="ts">
import { computed, onUnmounted, ref } from 'vue';
import BinaryClockCell from './BinaryClockCell.vue';

const numToSixBitBinary = (number: number) => {
    return number.toString(2).padStart(6, "0")
}
const binaryRows = [32, 16, 8, 4, 2, 1]
const now = ref(new Date())
const hours = computed(() => now.value.getHours())
const minutes = computed(() => now.value.getMinutes())
const seconds = computed(() => now.value.getSeconds())

const hoursBinary = computed(() => numToSixBitBinary(hours.value))
const minutesBinary = computed(() => numToSixBitBinary(minutes.value))
const secondsBinary = computed(() => numToSixBitBinary(seconds.value))

const time = setInterval(() => {
    now.value = new Date()
}, 1000)

onUnmounted(() => clearInterval(time))

</script>

<template>
    <div class="flex text-3xl gap-6">
        <div class="flex flex-col gap-3 items-center">
            <template v-for="(binaryNumber, index) in hoursBinary" :key="binaryNumber + index">
                <BinaryClockCell :active="binaryNumber === '1'" :binaryRow="binaryRows[index]" />
            </template>
            <span>{{ hours }}</span>
        </div>

        <div class="flex flex-col gap-3 items-center">
            <template v-for="(binaryNumber, index) in minutesBinary" :key="binaryNumber + index">
                <BinaryClockCell :active="binaryNumber === '1'" :binaryRow="binaryRows[index]" />
            </template>
            <span>{{ minutes }}</span>
        </div>

        <div class="flex flex-col gap-3 items-center">
            <template v-for="(binaryNumber, index) in secondsBinary" :key="binaryNumber + index">
                <BinaryClockCell :active="binaryNumber === '1'" :binaryRow="binaryRows[index]" />
            </template>
            <span>{{ seconds }}</span>
        </div>
    </div>
</template>