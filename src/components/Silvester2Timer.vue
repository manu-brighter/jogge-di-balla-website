<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <Countdown />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import { defineComponent } from 'vue'
import Countdown from "@/components/Countdown.vue";

export default defineComponent({
    components: {
        Countdown

    },
    // Your component's logic goes here
})
</script>

<style>
/* Your component-specific styles go here */
</style>
