---
layout: page
title: Livestream
permalink: /stream/
---

<div id="countdown" style="text-align: center; font-weight: bold; font-size: 48px;">
    <p id="timer"></p>
</div>

<script>
function startTimer(duration, display) {
    var timer = duration, days, hours, minutes, seconds;
    setInterval(function () {
        days = parseInt(timer / (24*60*60), 10);
        hours = parseInt((timer % (24*60*60)) / (60*60), 10);
        minutes = parseInt((timer % (60*60)) / 60, 10);
        seconds = parseInt(timer % 60, 10);

        days = days < 10 ? "0" + days : days;
        hours = hours < 10 ? "0" + hours : hours;
        minutes = minutes < 10 ? "0" + minutes : minutes;
        seconds = seconds < 10 ? "0" + seconds : seconds;

        display.textContent = days + "d " + hours + "h " + minutes + "m " + seconds + "s ";

        if (--timer < 0) {
            timer = duration; // Loop the countdown or stop the timer
        }
    }, 1000);
}

window.onload = function () {
    const deadline = new Date("Jun 14, 2024 17:00:00 GMT+0000").getTime();
    const now = new Date().getTime();
    const t = deadline - now;
    const seconds = Math.floor(t / 1000);

    startTimer(seconds, document.querySelector('#timer'));
};
</script>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube Live Stream</title>
</head>
<body>
    <h1>Watch Our Live Stream</h1>
    <div style="position:relative; padding-bottom:56.25%; height:0; overflow:hidden;">
        <iframe width="560" height="315" src="https://youtube.com/live/BjHV1RLVnvk" frameborder="0" allowfullscreen style="position:absolute; top:0; left:0; width:100%; height:100%;"></iframe>
    </div>
</body>