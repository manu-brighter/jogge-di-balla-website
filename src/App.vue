<script>

import Clock from '@/components/Clock.vue';
import Silvester2Timer from "@/components/Silvester2Timer.vue";

export default {
    components: {
        Silvester2Timer,
        Clock
    }
}

</script>

<template>
    <main>

        <Silvester2Timer />
<!--        <Clock />-->
<!--        <img src="@/assets/images/cursed-goomba.png">-->
    </main>

</template>

<style lang="scss">

@font-face {
    font-family: $roboto;
    src: url('@/assets/fonts/Roboto-Regular.ttf');
    font-weight: 500;
}

body,
html {
    background-color: $ciWhite;
    font-size: 10px;
    width: 100%;
	height: 100%;
    margin: 0;
	padding: 0;
    display: flex;
	justify-content: center;
	align-items: center;
}

* {
	box-sizing: border-box;
}

</style>
