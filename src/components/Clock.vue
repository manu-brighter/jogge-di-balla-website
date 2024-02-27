<template>
  <div class="clock wrapper">
      <div id="app">
          <h1>{{ currTime }}</h1>
      </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
          currTime: ""
      }
    },
      methods: {
          updateClock() {
              const now = new Date();
              const h = now.getHours().toString().padStart(2, "0");
              const m = now.getMinutes().toString().padStart(2, "0");
              const s = now.getSeconds().toString().padStart(2, "0");
              this.currTime = `${h}:${m}:${s}`;
          }
      },
      mounted () {
          this.updateClock();
          setInterval(this.updateClock, 1000);
    }
  }
</script>
<style>
h1 {
    color: white;
    font-size: 10rem;
}
</style>