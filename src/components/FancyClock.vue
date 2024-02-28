<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template >
    <div id="app">
        <div class="grid h-screen place-items-center back h-screen overflow-hidden">
            <div style="background-color: rgba(255, 255, 255, 30%);backdrop-filter: blur(12px); color: rgb(226 232 240);" class="font-bold text-base text-7xl tracking-widest rounded-lg p-10 backdrop-blur-sm bg-white/30 text-slate-200">
                <h1 class="flex justify-center">{{this.time}}</h1>
                <h3 v-if="date" class="text-2xl mt-3.5">{{dateBuilder()}}</h3>

                <div
                    v-if="show"
                    style="border-top-color:transparent"
                    class="w-16 h-16 border-4 border-slate-200 border-dashed rounded-full animate-spin"
                ></div>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    data() {
        return{
            time: "",
            date: false,
            show: true,
        }
    },
    methods: {
        getTime() {
            setInterval(() => { this.time = new Date().toLocaleTimeString()}, 1000)
        },
        showToggle() {
            setTimeout(() => {
                this.show = false
                this.date = true
            }, 1000)
        },
        dateBuilder() {
            let d = new Date();
            let months = [
                "January",
                "Feruary",
                "March",
                "April",
                "May",
                "June",
                "July",
                "August",
                "September",
                "October",
                "November",
                "December",
            ];
            let days = [
                "Sunday",
                "Monday",
                "Tuesday",
                "Wednesday",
                "Thursday",
                "Friday",
                "Saturday",
            ];

            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();

            return `${day} ${date} ${month} ${year}`;
        },
    },

    mounted() {
        this.getTime()
        this.showToggle()
    }
}
</script>

<style>
.back {
    background-color: #74EBD5;
    background-image: linear-gradient(90deg, #74EBD5 0%, #9FACE6 100%);
}

</style>
