<template>
    <main>
        <div class="background-container">
            <v-container>
                <Clock />
                <Silvester2Timer />
            </v-container>
        </div>
    </main>

</template>

<script>
import Silvester2Timer from "@/components/Silvester2Timer.vue";
import Clock from "@/components/Clock.vue";

export default {
    components: {
        Silvester2Timer,
        Clock
    },
    data() {
        return {
            darkModeEnabled: true // Set to true to enable dark mode, false for light mode
        };
    }
}

</script>

<style lang="scss">

@font-face {
    font-family: $roboto;
    src: url('@/assets/fonts/Roboto-Regular.ttf');
    font-weight: 500;
}

.background-container {
    /* Set background image */
    background-image: url('@/assets/images/background-sanft.jpg');
    background-size: cover;
    background-position: center;
    height: 100vh; /* Adjust height as needed */
}

</style>
