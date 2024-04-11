<template>
    <main class="background-container">
        <!-- Clock in the top-right corner -->
        <div class="clock-container">
            <Clock />
        </div>

        <!-- HappyTimeCountdown in the top-left corner -->
        <div class="happycountdown-container">
            <HappyTimeCountdown @countdown-finished="handleCountdownFinished" :startCountdown="/*startCountdown*/true" />
        </div>

        <!-- Countdown in the center of the screen -->
        <div class="countdown-center">
            <Countdown @start-countdown="handleStartCountdown" />
        </div>
    </main>
</template>


<script>
import {ref} from 'vue';
import Countdown from "@/components/Countdown.vue";
import HappyTimeCountdown from "@/components/HappyTimeCountdown.vue";
import Clock from "@/components/Clock.vue";

export default {
    components: {
        Countdown,
        HappyTimeCountdown,
        Clock
    },
    setup() {
        const startCountdown = ref(false);
        return { startCountdown };
    },
    methods: {
        handleStartCountdown() {
            this.startCountdown = true;
        },
        handleCountdownFinished() {
            this.startCountdown = false;
        }
    }
}

</script>

<style lang="scss">

html, body {
    overflow-y: hidden !important
}
.background-container {
    /* Set background image */
    background-image: url('@/assets/images/background-sanft.jpg');
    background-size: cover;
    background-position: center;
    height: 100vh;
    /* Adjust height as needed */
}

.clock-container {
    position: fixed;
    top: 20px;
    /* Adjust the top position as needed */
    right: 100px;
    /* Adjust the right position as needed */
    z-index: 1000;
    /* Ensure clock is above other elements */
}

.happycountdown-container {
    position: fixed;
    top: 20px;
    /* Adjust the top position as needed */
    left: 20px;
    /* Adjust the left position as needed */
    z-index: 1000;
    /* Ensure countdown is above other elements */
}

.countdown-center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
@media only screen and (max-width: 768px) {

    body {
        background-image: url('@/assets/images/background-sanft-phone.jpg');
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        margin: 0;
        padding: 0;
        height: 100vh;
    }

    .happycountdown-container {
        position: fixed;
        top: 86%;
        left:60%;
        transform: translate(-50%, -50%);
        z-index: 1000;
    }

    .clock-container {
        position: fixed;
        top: 2vh;
        left: 30%;
        transform: translateX(-50%);
        z-index: 1000;
    }

    .countdown-center {
        position: fixed;
        top: calc(25%);
        left: 107%;
        transform: translateX(-50%);
        z-index: 1000;
    }
}

</style>
