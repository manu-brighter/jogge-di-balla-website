<template>
    <v-container class="fill-height d-flex align-center justify-center" >
        <v-row justify="center">
            <v-col cols="12" md="6" sm="6">
                <v-card :class="{'countdown-card': true,  'background-image1': nextSilvesterName === 'irish', 'background-image2': nextSilvesterName === 'swiss', 'background-image3': nextSilvesterName === 'greek'}">
                    <v-card-text class="text-center glow-text">Countdown to Silvester 2</v-card-text>
                    <v-skeleton-loader v-if="isNaN(hours)" type="paragraph"/>
                    <v-card-text v-else class="text-center">
                        <div class="countdown glow-text">
                            <span>{{ formattedTime(hours) }}:{{ formattedTime(minutes) }}:{{
                                    formattedTime(seconds)
                                }}</span>
                        </div>
                    </v-card-text>
                    <v-card-text class="text-center glow-text">
                        Next Silvester is: <span>{{ nextSilvesterName }}</span>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import { defineComponent, ref, computed, watchEffect } from 'vue';

export default defineComponent({
    setup(props, context) {
        const currentDate = new Date();

        const swissCountdownDate = new Date();
        swissCountdownDate.setDate(currentDate.getDate());
        swissCountdownDate.setHours(24, 0, 1, 0);

        const irishCountdownDate = new Date();
        irishCountdownDate.setTime(swissCountdownDate.getTime() - (1 * 60 * 60 * 1000));

        const greekCountdownDate = new Date();
        greekCountdownDate.setTime(swissCountdownDate.getTime() + (1 * 60 * 60 * 1000));

        const timeRemaining = ref(getTimeRemaining());
        const nextSilvesterName = ref('');

        function getTimeRemaining(nextSilvesterDate) {
            const now = new Date().getTime();

            const difference = nextSilvesterDate - now;
            const hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((difference % (1000 * 60)) / 1000);
            if (hours === 0 && minutes === 0 && seconds === 0) {
                context.emit('start-countdown');
            }
            return { hours, minutes, seconds };
        }

        function changeNextSilvester(newName) {
            if (nextSilvesterName.value !== newName) {
                nextSilvesterName.value = newName;
            }
        }

        watchEffect(() => {
            const interval = setInterval(() => {
                const countdownDates = [
                    { date: irishCountdownDate, region: 'irish' },
                    { date: swissCountdownDate, region: 'swiss' },
                    { date: greekCountdownDate, region: 'greek' }
                ];

                const now = new Date();

                for (const item of countdownDates) {
                    if (now < item.date) {
                        changeNextSilvester(item.region);
                        timeRemaining.value = getTimeRemaining(item.date);
                        break;
                    }
                }
            }, 1000);

            return () => clearInterval(interval);
        });

        const hours = computed(() => timeRemaining.value.hours);
        const minutes = computed(() => timeRemaining.value.minutes);
        const seconds = computed(() => timeRemaining.value.seconds);

        const backgroundImageUrl = computed(() => {
            return '@/assets/images/Greece Flag.png'
            return `@/assets/images/${nextSilvesterName.value} Flag Blur.png`;
        });

        return {
            hours,
            minutes,
            seconds,
            nextSilvesterName,
            backgroundImageUrl
        };
    },
    methods: {
        formattedTime(time) {
            return time < 10 ? `0${time}` : time;
        }
    }
});
</script>

<style scoped>
.countdown-card {
    left: -31vh;
    width: 120vh; /* Adjust width as needed */
    height: 60vh;
    padding: 5vh;
    text-align: center; /* Center align the content */
    margin: 0 auto; /* Center the card horizontally */
}

.glow-text {
    text-shadow: 0 0 30px rgba(255, 255, 255, 1); /* Adjust the values as needed */
}

.background-image1 {
    background-image: url('@/assets/images/irish Flag Blur.png');
}

.background-image2 {
    background-image: url('@/assets/images/swiss Flag Blur.png');
}
.background-image3 {
    background-image: url('@/assets/images/greek Flag Blur.png');
}

.v-card {
    /*background-image: url('@/assets/images/swiss Flag Blur.png');*/
    background-size: cover;
    background-position: center;
    /*background-color: transparent;*/
    color: black;
    margin-top: 7vh;
}

.countdown {
    font-size: 24vh;
    margin: 0 auto; /* Center the countdown horizontally */
    display: inline-block; /* Make sure the countdown stays on a single line */
    margin-bottom: 2vh; /* Add space below the countdown */
    margin-top: 7vh; /* Add space top the countdown */
}

.text-center {
    margin: 4vh;
    font-size: 7vh;
}
</style>
