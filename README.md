<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Timer</title>
<style>
#timerInput {
    text-align: center;
}

#timerDisplay {
    text-align: center;
}

.timer-clock {
    display: inline-block;
    margin: 10px;
    font-size: 30px;
    font-family: 'Courier New', Courier, monospace;
}

.timer-input input {
    width: 50px;
    padding: 5px;
    font-size: 18px;
    text-align: center;
    margin: 0 5px;
}

.timer-buttons button {
    font-size: 18px;
    padding: 5px 10px;
    margin: 0 5px;
}
</style>
</head>
<body>
<div id="timerInput">
    <div class="timer-clock">
        <span id="hoursDisplay">00</span>:<span id="minutesDisplay">00</span>:<span id="secondsDisplay">00</span>
    </div>
    <div class="timer-input">
        <input type="number" id="hours" placeholder="시간">
        <input type="number" id="minutes" placeholder="분">
        <input type="number" id="seconds" placeholder="초">
    </div>
    <div class="timer-buttons">
        <button onclick="startTimer()">START</button>
    </div>
</div>
<div id="timerDisplay" style="display:none">
    <div class="timer-clock">
        <span id="timer"></span>
    </div>
    <div class="timer-buttons">
        <button onclick="stopTimer()">STOP</button>
        <button onclick="resetTimer()">RESET</button>
    </div>
</div>
<script>
let timer;
let hoursInput = document.getElementById('hours');
let minutesInput = document.getElementById('minutes');
let secondsInput = document.getElementById('seconds');
let timerDisplay = document.getElementById('timerDisplay');
let timerSpan = document.getElementById('timer');

function startTimer() {
    let hours = parseInt(hoursInput.value || 0);
    let minutes = parseInt(minutesInput.value || 0);
    let seconds = parseInt(secondsInput.value || 0);

    let totalSeconds = hours * 3600 + minutes * 60 + seconds;

    timerDisplay.style.display = 'block';
    document.getElementById('timerInput').style.display = 'none';

    timer = setInterval(function() {
        totalSeconds--;
        if (totalSeconds < 0) {
            clearInterval(timer);
            alert('타이머 종료!');
        } else {
            let h = Math.floor(totalSeconds / 3600);
            let m = Math.floor((totalSeconds % 3600) / 60);
            let s = totalSeconds % 60;

            timerSpan.textContent = `${h.toString().padStart(2, '0')}:${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
        }
    }, 1000);
}

function stopTimer() {
    clearInterval(timer);
}

function resetTimer() {
    clearInterval(timer);
    hoursInput.value = '';
    minutesInput.value = '';
    secondsInput.value = '';
    timerSpan.textContent = '';
    timerDisplay.style.display = 'none';
    document.getElementById('timerInput').style.display = 'block';
}
</script>
</body>
</html>
