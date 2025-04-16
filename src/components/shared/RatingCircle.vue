<template>
    <div class="flex flex-col items-center space-y-4">
        <!-- Thanh chọn giá trị -->
        <input type="range" min="1" max="5" step="1" v-model="value" class="w-48" />

        <!-- Vòng tròn đánh giá -->
        <div class="relative w-32 h-32">
            <!-- SVG vòng tròn -->
            <svg class="w-full h-full" viewBox="0 0 128 128">
                <!-- Vòng nền -->
                <circle class="text-orange-100" stroke="currentColor" stroke-width="10" fill="transparent" r="48" cx="64"
                    cy="64" />
                <!-- Vòng tiến trình -->
                <circle class="text-orange-400 transition-all duration-300" stroke="currentColor" stroke-width="10"
                    fill="transparent" r="48" cx="64" cy="64" :stroke-dasharray="circumference" :stroke-dashoffset="offset"
                    stroke-linecap="round" />
            </svg>

            <!-- Số chính giữa -->
            <div class="absolute inset-0 flex items-center justify-center text-3xl font-bold">
                {{ value }}
            </div>

            <!-- Ngôi sao -->
            <div class="absolute text-orange-400 transition-all duration-300" :style="starStyle">
                ⭐
            </div>
        </div>
    </div>
</template>
  
<script setup lang="ts">
import { ref, computed } from 'vue'

const value = ref(5)

const radius = 48
const circumference = 2 * Math.PI * radius

const offset = computed(() => {
    return circumference * (1 - value.value / 5)
})

// ✅ Tính góc theo chuẩn "3h = 0 độ", mỗi bước cách 72 độ
// value = 5 --> góc = 0 (3h)
// value = 4 --> góc = 72 (góc lệch xuống dưới phải)
// value = 3 --> góc = 144
// value = 2 --> góc = 216
// value = 1 --> góc = 288
const starStyle = computed(() => {
    const center = 64
    const r = 48
    const angleDeg = (5 - value.value) * 72
    const angleRad = (angleDeg * Math.PI) / 180
    const x = center + r * Math.cos(angleRad) - 10
    const y = center + r * Math.sin(angleRad) - 10

    return {
        top: `${y}px`,
        left: `${x}px`,
    }
})
</script>
  