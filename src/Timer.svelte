<script>
  import ProgressBar from './ProgressBar.svelte';
  import { createEventDispatcher } from 'svelte';
  const total = 20;
  let secondsLeft = total;
  let isRunning = false;
  $: progress = ((total - secondsLeft) / total) * 100;
  const disptach = createEventDispatcher();
  function startTimer() {
    isRunning = true;
    const timer = setInterval(() => {
      secondsLeft -= 1;
      if (secondsLeft === 0) {
        clearInterval(timer);
        isRunning = false;
        secondsLeft = total;
        disptach('end', 'end timer');
      }
    }, 1000);
  }
</script>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left: {secondsLeft}</h2>
</div>

<ProgressBar {progress} />

<div bp="grid">
  <button
    bp="offset-5@md 4@md 12@sm"
    on:click={startTimer}
    disabled={isRunning}
    class="start">Start</button
  >
</div>

<style>
  h2 {
    margin: 0;
  }
  .start {
    background-color: rgb(154, 73, 73);
    width: 100%;
    margin: 10px 0;
  }

  .start[disabled] {
    background-color: rgb(194, 194, 194);
    cursor: not-allowed;
  }
</style>
