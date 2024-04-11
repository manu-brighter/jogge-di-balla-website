<template>
    <v-container class="fill-height d-flex align-center justify-center">
        <v-row justify="center">
            <v-col cols="12" md="6" sm="6">
                <v-card :class="['countdown-card', backgroundImageClass]">
                    <v-card-text class="text-center glow-text">Countdown zum Silvester 2.0</v-card-text>
                    <v-skeleton-loader v-if="isNaN(hours)" type="paragraph"/>
                    <v-card-text v-else class="text-center">
                        <div class="countdown glow-text">
                            <span>{{ formattedTime(hours) }}:{{ formattedTime(minutes) }}:{{ formattedTime(seconds) }}</span>
                        </div>
                    </v-card-text>
                    <v-card-text class="text-center glow-text">
                        Bis zum <span>{{ nextSilvesterText }}  </span><br><br><br><br>Silvester
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
        swissCountdownDate.setHours(16, 20, 0, 0);

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
                console.log("lkjasdfkjhfkj")
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

        const nextSilvesterText = computed(() => {
            switch (nextSilvesterName.value) {
                case 'irish':
                    return 'irischen';
                case 'swiss':
                    return 'schweizer';
                case 'greek':
                    return 'griechischen';
                default:
                    return '';
            }
        });

        const backgroundImageClass = computed(() => {
            switch (nextSilvesterName.value) {
                case 'irish':
                    return 'background-image1';
                case 'swiss':
                    return 'background-image2';
                case 'greek':
                    return 'background-image3';
                default:
                    return '';
            }
        });

        return {
            hours,
            minutes,
            seconds,
            nextSilvesterName,
            nextSilvesterText,
            backgroundImageClass
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
    text-shadow: 0 0 30px black; /* Adjust the values as needed */
}

.v-card {
    background-size: cover;
    background-position: center;
    color: navajowhite;
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

.background-image1 {
    background-image: url('@/assets/images/irish Flag Blur.png');
}

.background-image2 {
    background-image: url('@/assets/images/swiss Flag Blur.png');
}
.background-image3 {
    background-image: url('@/assets/images/greek Flag Blur.png');
}

@media only screen and (max-width: 768px) {
    .countdown-card {
        width: 80vw; /* Adjust width as needed */
        height: 45vh; /* Adjust height as needed */
        padding: 0px;
        margin: 0px;

    }
    .countdown {
        font-size: 14vw; /* Adjust font size as needed */
    }
    .text-center {
        font-size: 8vw; /* Adjust font size as needed */
        width: 80vw;
    }
    .v-card-text {
        padding-left: 0px;
        margin-left: 0px;
        margin-top: 8px;
        margin-bottom: 10px;
        padding-top: 10px;
        padding-bottom: 20px;
    }
}
</style>
