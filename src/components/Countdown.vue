<template>
    <v-container>
        <v-row justify="center">
            <v-col cols="12" sm="6" md="6">
                <v-card>
                    <v-card-title class="text-center">Countdown to Silvester 2</v-card-title>
                    <v-skeleton-loader v-if="isNaN(hours)" type="paragraph" />
                    <v-card-text v-else class="text-center" >
                        <div class="countdown">
                            <span>{{ hours }}</span> hours
                            <span>{{ minutes }}</span> minutes
                            <span>{{ seconds }}</span> seconds
                        </div>
                    </v-card-text>
                    <v-card-text class="text-center" >
                        Next Silvester is: <span>{{ nextSilvesterName }}</span>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import { defineComponent, ref, computed, watchEffect } from 'vue'

export default defineComponent({
    components: {

    },
    setup(props, context) {
        // Current date
        const currentDate = new Date();

        // Tomorrow's date at 00:00:00
        const swissCountdownDate = new Date();
        swissCountdownDate.setDate(currentDate.getDate());
        swissCountdownDate.setHours(24, 0, 1, 0); // set silvester time here

        // One hour before
        const greekCountdownDate = new Date();
        greekCountdownDate.setTime(swissCountdownDate.getTime() - (1 * 60 * 60 * 1000));

        // One hour ahead
        const irishCountdownDate = new Date();
        irishCountdownDate.setTime(swissCountdownDate.getTime() + (1 * 60 * 60 * 1000));

        const timeRemaining = ref(getTimeRemaining())
        const nextSilvesterName = ref('');

        function getTimeRemaining(nextSilvesterDate) {
            const now = new Date().getTime()

            const difference = nextSilvesterDate - now
            const hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
            const minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60))
            const seconds = Math.floor((difference % (1000 * 60)) / 1000)
            if (hours === 0 && minutes === 0 && seconds === 0){
                context.emit('start-countdown');
            }
            return { hours, minutes, seconds }
        }

        function changeNextSilvester(newName) {
            if (nextSilvesterName.value !== newName){
                nextSilvesterName.value = newName;
            }
        }


        watchEffect(() => {
            const interval = setInterval(() => {
                const countdownDates = [
                    { date: greekCountdownDate, region: 'greek' },
                    { date: swissCountdownDate, region: 'swiss' },
                    { date: irishCountdownDate, region: 'irish' }
                ];

                const now = new Date();

                for (const item of countdownDates) {
                    if (now < item.date) {
                        changeNextSilvester(item.region);
                        timeRemaining.value = getTimeRemaining(item.date);
                        break;
                    }
                }

            }, 1000)

            return () => clearInterval(interval)
        })

        const hours = computed(() => timeRemaining.value.hours)
        const minutes = computed(() => timeRemaining.value.minutes)
        const seconds = computed(() => timeRemaining.value.seconds)

        return {
            hours,
            minutes,
            seconds,
            nextSilvesterName
        }
    }
})
</script>

<style scoped>
.countdown {
    font-size: 24px;
}
</style>
