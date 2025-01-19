# -PRODIGY_WD_02
# HTML FILES
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link rel="stylesheet" href="styles1.css">
</head>
<body>
    <div class="stopwatch">
        <div class="display" id="display">00:00:00</div>
        <div class="controls">
            <button id="startStopBtn" onclick="startStop()">Start</button>
            <button onclick="reset()">Reset</button>
            <button onclick="lap()">Lap</button>
        </div>
        <ul id="laps"></ul>
    </div>
    <script src="script1.js"></script>
</body>
</html>

#CSS FILES

body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f0f0f0;
}

.stopwatch {
    text-align: center;
}

.display {
    font-size: 48px;
    margin-bottom: 20px;
}

.controls button {
    font-size: 16px;
    padding: 10px 20px;
    margin: 5px;
    cursor: pointer;
}

#laps {
    list-style: none;
    padding: 0;
}

#laps li {
    font-size: 18px;
    margin: 5px 0;
}

#JAVASCRIPT FILES

let timer;
let isRunning = false;
let startTime;
let elapsedTime = 0;
let lapCounter = 1;

function startStop() {
    const startStopBtn = document.getElementById('startStopBtn');
    
    if (isRunning) {
        clearInterval(timer);
        isRunning = false;
        startStopBtn.textContent = 'Start';
    } else {
        startTime = Date.now() - elapsedTime;
        timer = setInterval(updateDisplay, 10);
        isRunning = true;
        startStopBtn.textContent = 'Pause';
    }
}

function reset() {
    clearInterval(timer);
    isRunning = false;
    elapsedTime = 0;
    document.getElementById('display').textContent = '00:00:00';
    document.getElementById('startStopBtn').textContent = 'Start';
    document.getElementById('laps').innerHTML = '';
    lapCounter = 1;
}

function lap() {
    if (isRunning) {
        const lapTime = document.getElementById('display').textContent;
        const lapItem = document.createElement('li');
        lapItem.textContent = `Lap ${lapCounter}: ${lapTime}`;
        document.getElementById('laps').appendChild(lapItem);
        lapCounter++;
    }
}

function updateDisplay() {
    elapsedTime = Date.now() - startTime;
    const milliseconds = Math.floor((elapsedTime % 1000) / 10).toString().padStart(2, '0');
    const seconds = Math.floor((elapsedTime / 1000) % 60).toString().padStart(2, '0');
    const minutes = Math.floor((elapsedTime / 60000) % 60).toString().padStart(2, '0');
    document.getElementById('display').textContent = `${minutes}:${seconds}:${milliseconds}`;
}
