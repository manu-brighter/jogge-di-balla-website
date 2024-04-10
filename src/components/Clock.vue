<!-- Clock.vue -->
<template>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="6" md="4">
          <v-card class="clock-card">
            <v-card-title class="text-center">Current Time</v-card-title>
            <v-card-text class="text-center">
              <div class="time">{{ currentTime }}</div>
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
    background-color: darkslategray;
    color: greenyellow;
}

.clock-card {
    width: fit-content;
    padding: 20px;
    margin-right: 14vh;
    width: 30vh;
    height: 15vh;
}

.v-card-title {
    font-size: 3vh;
}

.time {
    padding-top: 1vh;
    font-size: 5vh;
}
</style>
