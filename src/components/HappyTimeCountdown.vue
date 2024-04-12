<template>
    <v-container v-if="minutes !== 0 && seconds !== 0">
        <v-row justify="center">
            <v-col cols="12" sm="6" md="4">
                <v-card class="countdown-card" v-if="startCountdown">
                    <v-card-text class="text-center glow-text">Happy Time</v-card-text>
                    <v-card-text class="text-center">
                        <div class="countdown glow-text">
                            <span>{{ formattedTime(minutes) }}</span> : <span>{{ formattedTime(seconds) }}</span>
                        </div>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
    <v-container v-else>
        <v-img src="/assets/images/Website Pics/miniongif3.gif"></v-img>
    </v-container>
</template>


<script>
import { defineComponent, ref, watchEffect } from 'vue';

export default defineComponent({
    props: {
        startCountdown: {
            type: Boolean,
            default: false
        }
    },
    setup(props, context) {
        const minutes = ref(15);
        const seconds = ref(0);

        watchEffect(() => {
            if (props.startCountdown) {
                const interval = setInterval(() => {
                    if (seconds.value === 0) {
                        if (minutes.value === 0) {
                            clearInterval(interval);
                            context.emit('countdown-finished')
                        } else {
                            minutes.value--;
                            seconds.value = 59;
                        }
                    } else {
                        seconds.value--;
                    }
                }, 1000);
                return () => clearInterval(interval);
            }
        });

        return { minutes, seconds };
    },
    methods: {
        formattedTime(time) {
            return time < 10 ? `0${time}` : time;
        }
    }
});
</script>

<style scoped>
.v-card {
    background-color: darkslategrey;
    color: navajowhite;
    left: -5vh;
}

.countdown-card {
    width: 30vh;
    height: 15vh;
    padding: 20px;
}

.v-card-text {
    font-size: 3vh;
}

.countdown {
    padding-top: 0vh;
    font-size: 6vh;
}

.glow-text {
    text-shadow: 0 0 30px black; /* Adjust the values as needed */
}
@media only screen and (max-width: 768px) {
    .countdown-card {
        width: 80vw; /* Adjust width as needed */
        height: 16vh; /* Adjust height as needed */
        padding: 2vw; /* Adjust padding as needed */
    }
    .text-center {
        font-size: 7vw; /* Adjust font size as needed */
    }
}
</style>
