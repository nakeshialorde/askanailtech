mediaPlayer = document.getElementById('media-video');
document.addEventListener("DOMContentLoaded", function() {
  initialiseMediaPlayer();
}, false);
mediaPlayer.addEventListener('timeupdate', updateProgressBar, false);

function initialiseMediaPlayer() {
  mediaPlayer.controls = false;
}

function togglePlayPause() {
  var btn = document.getElementById('play-pause-button');
  var ovr = document.getElementById('play-disp');
  var avi = document.getElementById('user-avi');
  if (mediaPlayer.paused || mediaPlayer.ended) {
    btn.title = 'pause';
    ovr.innerHTML = '<span class="fa fa-pause"></span>';
    ovr.style.textShadow = '0 0 0 #fff, 0 0.5px 1px #000';
    avi.style.transform = "scale(1)";
    mediaPlayer.play();
  } else {
    btn.title = 'play';
    ovr.innerHTML = '<span class="fa fa-play"></span>';
    avi.style.transform = "scale(0)";
    ovr.style.textShadow = 'none';
    mediaPlayer.pause();
  }
}

function updateProgressBar() {
  var progressBar = document.getElementById('play-bar');
  var percentage = Math.floor((100 / mediaPlayer.duration) *
    mediaPlayer.currentTime);
  progressBar.style.width = percentage + "%";
}
