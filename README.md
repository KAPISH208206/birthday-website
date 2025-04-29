<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
  <title>Happy Birthday, Mom!</title>
  <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Open+Sans&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Open Sans', sans-serif;
      background: linear-gradient(to right, #ff8a65, #d81b60);
      text-align: center;
      color: #fff;
      overflow-x: hidden;
    }
    h1 {
      font-family: 'Great Vibes', cursive;
      font-size: 2.5em;
      margin-top: 1.5em;
    }
    .message {
      font-size: 1.1em;
      margin: 15px auto;
      max-width: 90%;
    }
    .funny {
      font-size: 1em;
      margin-top: 15px;
      color: #ffeb3b;
    }
    .slideshow {
      margin: 20px auto;
      width: 90%;
      max-width: 400px;
      border-radius: 20px;
      overflow: hidden;
    }
    .slideshow img {
      width: 100%;
      display: none;
      border-radius: 20px;
    }
    .slideshow img.active {
      display: block;
    }
    #audio-player {
      display: none;
    }
    #toggle-audio {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: #fff;
      color: #d81b60;
      border: none;
      font-weight: bold;
      font-size: 1em;
      border-radius: 10px;
      cursor: pointer;
    }
    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 10;
    }
  </style>
</head>
<body>

  <h1>Happy Birthday, Mom! 🎉</h1>
  <div class="message">
    <p>Thank you for being my strength, my guide, and my forever friend. May this year bring you as much joy as you bring to everyone around you. You deserve the world. 💖</p>
    <div class="funny">Your age just got incremented — but don’t worry, it’s still within integer limits! 😂🎂🎈</div>
  </div>

  <div class="slideshow">
    <img src="1.jpeg" class="active" alt="Mom 1" />
    <img src="2.jpeg" alt="Mom 2" />
    <img src="3.jpeg" alt="Mom 3" />
    <img src="4.jpeg" alt="Mom 4" />
    <img src="5.jpeg" alt="Mom 5" />
    <img src="6.jpeg" alt="Mom 6" />
    <img src="7.jpeg" alt="Mom 7" />
    <img src="8.jpeg" alt="Mom 8" />
    <img src="9.jpeg" alt="Mom 9" />
  </div>

  <button id="toggle-audio">🎵 Tap to Play Audio</button>
  <audio id="audio-player"></audio>

  <canvas id="confetti-canvas"></canvas>

  <script>
    // Slideshow
    const images = document.querySelectorAll('.slideshow img');
    let currentImage = 0;
    setInterval(() => {
      images[currentImage].classList.remove('active');
      currentImage = (currentImage + 1) % images.length;
      images[currentImage].classList.add('active');
    }, 3000);

    // Confetti
    const canvas = document.getElementById('confetti-canvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const pieces = Array.from({ length: 100 }, () => ({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 6 + 4,
      d: Math.random() * 100,
      color: `hsl(${Math.random() * 360}, 100%, 50%)`,
      tilt: Math.floor(Math.random() * 10) - 10
    }));

    function drawConfetti() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      pieces.forEach(p => {
        ctx.beginPath();
        ctx.fillStyle = p.color;
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fill();
      });
      updateConfetti();
    }

    function updateConfetti() {
      pieces.forEach(p => {
        p.y += Math.cos(p.d) + 1 + p.r / 2;
        p.x += Math.sin(p.d);
        if (p.y > canvas.height) {
          p.y = 0;
          p.x = Math.random() * canvas.width;
        }
      });
    }

    setInterval(drawConfetti, 30);

    // Audio
    const audioPlayer = document.getElementById('audio-player');
    const toggleBtn = document.getElementById('toggle-audio');
    const audioSources = ['kapishvoice.ogg', 'avamvoice.ogg'];
    let currentIndex = 0;
    let isPlaying = false;

    function playNextAudio() {
      currentIndex = (currentIndex + 1) % audioSources.length;
      audioPlayer.src = audioSources[currentIndex];
      audioPlayer.play();
    }

    audioPlayer.addEventListener('ended', playNextAudio);

    toggleBtn.addEventListener('click', () => {
      if (!isPlaying) {
        audioPlayer.src = audioSources[currentIndex];
        audioPlayer.play();
        toggleBtn.textContent = '⏸ Pause Audio';
        isPlaying = true;
      } else {
        audioPlayer.pause();
        toggleBtn.textContent = '▶️ Play Audio';
        isPlaying = false;
      }
    });
  </script>

</body>
</html>
