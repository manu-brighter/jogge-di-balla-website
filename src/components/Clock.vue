<!-- Clock.vue -->
<template>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="6" md="4">
          <v-card class="clock-card">
            <v-card-text class="text-center glow-text">Uhrzeit MESZ</v-card-text>
            <v-card-text class="text-center">
              <div class="time glow-text">{{ currentTime }}</div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
    components: {
    },
    setup() {
        const currentTime = ref('');

        // Update current time every second
        setInterval(() => {
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            const seconds = now.getSeconds().toString().padStart(2, '0');
            currentTime.value = `${hours}:${minutes}:${seconds}`;
        }, 1000);

        return { currentTime };
    }
});
</script>

<style scoped>
.v-card {
    background-color: darkslategrey;
    color: navajowhite;
}

.clock-card {
    width: fit-content;
    padding: 20px;
    margin-right: 14vh;
    width: 30vh;
    height: 15vh;
}

.v-card-text {
    font-size: 3vh;
}

.time {
    padding-top: 0vh;
    font-size: 5vh;
}

.glow-text {
    text-shadow: 0 0 30px black; /* Adjust the values as needed */
}
@media only screen and (max-width: 768px) {
    .clock-card {
        width: 80vw; /* Adjust width as needed */
        height: 16vh; /* Adjust height as needed */
        padding: 2vw; /* Adjust padding as needed */
    }
    .text-center {
        font-size: 7vw; /* Adjust font size as needed */
    }
}
</style>
