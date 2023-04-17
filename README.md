# CodeClause_Timer_-_Stopwatch




/*  HTML CODE*/

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer and stopwatch</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    

    <div class="timer-container">
        <h1>Timer</h1>
        <div class="display">
            <span class="hours">00</span> :
            <span class="minutes">00</span> :
            <span class="seconds">00</span>
        </div>
        <button class="start-btn">Start</button>
        <button class="stop-btn">Stop</button>
        <button class="reset-btn">Reset</button>
    </div>

<div id="stopwatch">
<h1>Stopwatch</h1>
<p id="display">0.00</p>
<button onclick="start()">Start</button>
<button onclick="stop()">Stop</button>
<button onclick="reset()">Reset</button>
</div>

<script src="script.js"></script>

</body>
</html>




/*CSS code*/

.timer-container {
  margin: 20px;
  text-align: center;
}

.display {
  font-size: 4em;
}

#stopwatch{
  margin: 20px;
  text-align: center;

}

button {
  font-size: 1.2em;
  margin: 10px;
  padding: 10px;
  border: none;
  border-radius: 5px;
  background-color: #0077cc;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #0066b2;
}


/*JAVASCRIPT CODE*/



/*timer*/
let timerInterval;
let timerSeconds = 0;
let timerMinutes = 0;
let timerHours = 0;

const timerDisplay = document.querySelector('.timer-container .display');
const timerStartBtn = document.querySelector('.timer-container .start-btn');
const timerStopBtn = document.querySelector('.timer-container .stop-btn');
const timerResetBtn = document.querySelector('.timer-container .reset-btn');

timerStartBtn.addEventListener('click', startTimer);
timerStopBtn.addEventListener('click', stopTimer);
timerResetBtn.addEventListener('click', resetTimer);

function startTimer() {
  timerInterval = setInterval(incrementTimer, 1000);
  timerStartBtn.disabled = true;
}

function stopTimer() {
  clearInterval(timerInterval);
  timerStartBtn.disabled = false;
}

function resetTimer() {
  clearInterval(timerInterval);
  timerSeconds = 0;
  timerMinutes = 0;
  timerHours = 0;
  updateTimerDisplay();
  timerStartBtn.disabled = false;
}

function incrementTimer() {
  timerSeconds++;
  if (timerSeconds === 60) {
    timerMinutes++;
    timerSeconds = 0;
  }
  if (timerMinutes === 60) {
    timerHours++;
    timerMinutes = 0;
  }
  updateTimerDisplay();
}

function updateTimerDisplay() {
  const secondsStr = timerSeconds < 10 ? '0' + timerSeconds.toString() : timerSeconds.toString();
  const minutesStr = timerMinutes < 10 ? '0' + timerMinutes.toString() : timerMinutes.toString();
  const hoursStr = timerHours < 10 ? '0' + timerHours.toString() : timerHours.toString();
  timerDisplay.innerHTML = `<span class="hours">${hoursStr}</span> : <span class="minutes">${minutesStr}</span> : <span class="seconds">${secondsStr}</span>`;
}




//STOPwatch


let startTime, endTime, elapsed, intervalId;

function start() {
  startTime = new Date();
  intervalId = setInterval(update, 10);
}

function stop() {
  clearInterval(intervalId);
  endTime = new Date();
  elapsed = (endTime.getTime() - startTime.getTime()) / 1000;
}

function update() {
  let currentTime = new Date();
  elapsed = (currentTime.getTime() - startTime.getTime()) / 1000;
  document.getElementById("display").innerHTML = elapsed.toFixed(2);
}

function reset() {
  startTime = null;
  endTime = null;
  elapsed = 0;
  clearInterval(intervalId);
  document.getElementById("display").innerHTML = elapsed.toFixed(2);
}




