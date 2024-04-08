<template>
    <v-container>
        <v-row justify="center">
            <v-col cols="12" sm="6" md="4">
                <v-card class="countdown-card" v-if="startCountdown">
                    <v-card-title class="text-center">Happy Time</v-card-title>
                    <v-card-text class="text-center">
                        <div class="countdown">
                            <span>{{ formattedTime(minutes) }}</span> : <span>{{ formattedTime(seconds) }}</span>
                        </div>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
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
    components: {
    },
    setup(props, context) {
        const minutes = ref(0);
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
    background-color: red;
    color: white;
}

.countdown-card {
    width: 200px;
    padding: 20px;
}

.countdown {
    font-size: 40px;
}
</style>
