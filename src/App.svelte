<script>
  import Timer from './Timer.svelte';
  import HowTo from './HowTo.svelte';
  let audio;
  function timerEnds(e) {
    console.log(e.detail);
    audio.play();
  }
</script>

<h1>Handwashing app</h1>
<Timer on:end={timerEnds} />
<HowTo />

<audio bind:this={audio}>
  <source src="sound.wav" />
</audio>

<style>
  h1 {
    text-align: center;
  }
</style>
