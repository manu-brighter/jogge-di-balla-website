<script>

import Clock from '@/components/Clock.vue';

export default {
    components: {
        Clock
    }
}

</script>

<template>
    <main>
        <Clock />
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
    background-color: $second;
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
