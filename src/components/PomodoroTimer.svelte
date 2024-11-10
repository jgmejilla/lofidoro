<script>    
    let minutes = 25;
    let time = minutes * 60; 
    let timer;
    let isRunning = false;
    
    function sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
  
    async function startTimer() {
      if (!isRunning) {
        isRunning = true;
        while (time > 0) {
          await sleep(1000);
          time -= 1;
        }
        isRunning = false
      }
    }
  
    function reset() {
      function resetText() {
  
      }
  
      function resetTimer() {
        clearInterval(timer);
        time = minutes * 60;
        isRunning = false;
      }
  
      resetText();
      resetTimer();
    }
  
    function formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const secs = seconds % 60;
      let newTime = `${minutes}:${secs < 10 ? '0' : ''}${secs}`
      document.title = newTime
      return newTime;
    }
  </script>
  
  <div class="pomodoro-timer">
    <div class="time-display">{formatTime(time)}</div>
    <button on:click={startTimer} disabled={isRunning}>Start</button>
    <button on:click={reset}>Reset</button>
  </div>
    
  <style>
    .pomodoro-timer {
      margin: 20px;
      text-align: center;
    }
    .time-display {
      font-size: 5em;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      margin: 5px;
    }
  </style>