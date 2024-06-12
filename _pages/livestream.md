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
    <style>
        .video-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh; /* Adjust based on your needs */
        }
        .responsive-iframe {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 aspect ratio */
            height: 0;
            width: 100%;
            max-width: 560px; /* Adjust based on your needs */
            overflow: hidden;
        }
        .responsive-iframe iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
    </style>
</head>
<body>
    <h1 style="text-align: center;">Watch Our Live Stream</h1>
    <div class="video-container">
        <div class="responsive-iframe">
            <iframe width="560" height="315" src="https://www.youtube.com/embed/BjHV1RLVnvk?si=iCzTVC3WdwkOY26T" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
        </div>
    </div>
</body>

