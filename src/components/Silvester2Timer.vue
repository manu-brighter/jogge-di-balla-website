<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <HappyTimeCountdown @countdown-finished="handleCountdownFinshed" :startCountdown="startCountdown" />
            </v-col>
            <v-col cols="12">
                <Countdown @start-countdown="handleStartCountdown" />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import { defineComponent, ref } from 'vue'
import Countdown from "@/components/Countdown.vue";
import HappyTimeCountdown from "@/components/HappyTimeCountdown.vue";

export default defineComponent({
    components: {
        HappyTimeCountdown,
        Countdown
    },

    setup() {
        const startCountdown = ref(false);
        return { startCountdown };
    },
    methods: {
        handleStartCountdown() {
            this.startCountdown = true;
        },
        handleCountdownFinshed() {
            this.startCountdown = false;
        }
    }
})
</script>

<style>
/* Your component-specific styles go here */
</style>
