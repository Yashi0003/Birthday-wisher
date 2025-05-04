<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Birthday Wisher</title>
  <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Roboto&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(135deg, #8e44ad, #f1c40f);
      overflow: hidden;
    }

    .container {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      text-align: center;
      padding: 20px;
    }

    .hidden {
      display: none;
    }

    h1 {
      font-family: 'Great Vibes', cursive;
      font-size: 3rem;
      color: #fff;
      animation: fadeInDown 1.5s ease-in-out;
    }

    p {
      color: #fce4ec;
      font-size: 1.2rem;
      margin: 10px 0;
      animation: fadeInUp 1.5s ease-in-out;
    }

    input {
      padding: 12px;
      font-size: 1rem;
      border: none;
      border-radius: 5px;
      margin-bottom: 10px;
      outline: none;
    }

    button, .share-btn {
      padding: 12px 20px;
      background: #fff;
      color: #8e44ad;
      font-weight: bold;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin: 8px;
      transition: 0.3s ease;
    }

    button:hover, .share-btn:hover {
      background-color: #f3e5f5;
    }

    #confetti-canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 999;
      pointer-events: none;
    }

    @keyframes fadeInDown {
      0% { opacity: 0; transform: translateY(-40px); }
      100% { opacity: 1; transform: translateY(0); }
    }

    @keyframes fadeInUp {
      0% { opacity: 0; transform: translateY(40px); }
      100% { opacity: 1; transform: translateY(0); }
    }

    strong {
      color: #ffd700;
      font-family: 'Great Vibes', cursive;
    }
  </style>
</head>
<body>

<canvas id="confetti-canvas"></canvas>

<!-- Step 1: Name Input Screen -->
<div class="container" id="input-screen">
  <h1>🎉 Birthday Wisher 🎂</h1>
  <p>Enter the name of the birthday person</p>
  <input type="text" id="nameInput" placeholder="e.g. Anjali">
  <br>
  <button onclick="showBirthdayWish()">Wish Now</button>
</div>

<!-- Step 2: Birthday Message Screen -->
<div class="container hidden" id="wish-screen">
  <h1 id="birthdayMessage"></h1>
  <p id="quote1"></p>
  <p id="quote2"></p>
  <p id="quote3"></p>
  <a id="whatsapp-share" class="share-btn" target="_blank">📱 Share on WhatsApp</a>
</div>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
<script>
  const nameInput = document.getElementById('nameInput');
  const inputScreen = document.getElementById('input-screen');
  const wishScreen = document.getElementById('wish-screen');
  const birthdayMessage = document.getElementById('birthdayMessage');
  const whatsappBtn = document.getElementById('whatsapp-share');

  const quotes = [
    "Count your life by smiles, not tears. Count your age by friends, not years.",
    "Today is not the end of another year, but the start of a new one.",
    "Wishing you a day filled with love, laughter, and cake!"
  ];

  function showBirthdayWish() {
    const name = nameInput.value.trim();
    if (name === "") {
      alert("Please enter a name!");
      return;
    }

    inputScreen.classList.add("hidden");
    wishScreen.classList.remove("hidden");

    birthdayMessage.innerHTML = `🎂 Happy Birthday, <strong>${name}</strong>! 🎉`;
    document.getElementById('quote1').innerText = quotes[0];
    document.getElementById('quote2').innerText = quotes[1];
    document.getElementById('quote3').innerText = quotes[2];

    const shareText = `🎉 Happy Birthday, ${name}! 🎂\n\n${quotes.join("\n")}\n\n🎁 Sent via Birthday Wisher App`;
    const whatsappLink = `https://wa.me/?text=${encodeURIComponent(shareText)}`;
    whatsappBtn.href = whatsappLink;

    launchConfetti();
  }

  function launchConfetti() {
    const duration = 10 * 1000;
    const end = Date.now() + duration;

    (function frame() {
      confetti({
        particleCount: 4,
        angle: 60,
        spread: 70,
        origin: { x: 0 }
      });
      confetti({
        particleCount: 4,
        angle: 120,
        spread: 70,
        origin: { x: 1 }
      });

      if (Date.now() < end) {
        requestAnimationFrame(frame);
      }
    })();
  }
</script>
</body>
</html>
