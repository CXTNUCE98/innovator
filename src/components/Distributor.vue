<script setup lang="ts">
import Kaching from "@/public/kaching.png"
import Amazon from "@/public/amazon.png"
import Anti from "@/public/anti_hang_gia.png"
import Tiktok from "@/public/tiktok.png"
import Zecom from "@/public/zecom.png"
import Netflix from "@/public/netflix.png"

const distributor = [
    Kaching,
    Amazon,
    Anti,
    Tiktok,
    Zecom,
    Netflix,
    // Airbnb,
    // Turkish,
    // Swiss
]

</script>

<template>
    <div class="marquee py-30px">
        <div class="marquee-content flex justify-around w-full ">
            <template v-for="i in distributor" :key="i">
                <img :src="i" class="marquee-item object-contain w-auto h-40px">
            </template>
            <template v-for="i in distributor" :key="'dup-' + i">
                <img :src="i" class="marquee-item object-contain w-auto h-40px">
            </template>
        </div>
    </div>
</template>

<style scoped>
.marquee {
    overflow: hidden;
    white-space: nowrap;
    width: 100%;
}

.marquee-content {
    display: flex;
    align-items: center;
}

.marquee-item {
    flex-shrink: 0;
    margin-right: 220px;
}

@keyframes marquee-animation {
    0% {
        transform: translateX(0);
    }

    100% {
        transform: translateX(-50%);
    }
}

.marquee-content {
    animation: marquee-animation 10s linear infinite;
}
</style>