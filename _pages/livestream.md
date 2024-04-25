---
layout: page
title: Livestream
permalink: /livestream/
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
