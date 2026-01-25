<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
  body {
    margin: 0;
    font-family: 'Arial', sans-serif;
    background: black;
    color: #e0e0e0;
    overflow: hidden;
  }

  /* Flying dots background */
  .dot {
    position: absolute;
    background: white;
    border-radius: 50%;
    opacity: 0.8;
    animation: moveDot linear infinite;
  }
  @keyframes moveDot {
    0% { transform: translateY(0) translateX(0); }
    100% { transform: translateY(120vh) translateX(50vw); }
  }

  header {
    text-align: center;
    padding: 20px;
    background: #111;
    border-bottom: 2px solid #444;
    position: relative;
    z-index: 2;
  }
  header h1 {
    margin: 0;
    color: #f0f0f0;
  }
  header p {
    margin: 5px 0 0;
    font-size: 0.9rem;
    color: #ccc;
  }

  .container {
    max-width: 700px;
    margin: 30px auto;
    padding: 20px;
    background: #1a1a1a;
    border-radius: 15px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.5);
    position: relative;
    z-index: 2;
  }

  h2 {
    text-align: center;
    color: #f0f0f0;
    margin-bottom: 20px;
  }

  .item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #222;
    margin: 10px 0;
    padding: 12px 20px;
    border-radius: 10px;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .item:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 15px rgba(255,255,255,0.2);
  }

  .item-name { font-weight: bold; font-size: 1rem; color: #fff; }
  .item-price { color: #aaa; font-weight: bold; }

  .buy-btn, .tiktok-btn {
    background: #333;
    color: #fff;
    border: none;
    padding: 8px 14px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
    text-decoration: none;
    transition: all 0.3s;
  }
  .buy-btn:hover, .tiktok-btn:hover {
    background: #555;
    transform: scale(1.05);
  }

  .tiktok-btn { display: inline-block; margin: 20px auto; text-align: center; }

  footer {
    text-align: center;
    padding: 15px;
    margin-top: 30px;
    color: #aaa;
    font-size: 0.9rem;
    position: relative;
    z-index: 2;
  }
</style>
</head>
<body>

<!-- Flying dots -->
<script>
  const numDots = 80;
  for (let i = 0; i < numDots; i++) {
    const dot = document.createElement('div');
    dot.classList.add('dot');
    const size = Math.random() * 3 + 1;
    dot.style.width = size + 'px';
    dot.style.height = size + 'px';
    dot.style.top = Math.random() * window.innerHeight + 'px';
    dot.style.left = Math.random() * window.innerWidth + 'px';
    dot.style.animationDuration = (20 + Math.random() * 40) + 's';
    document.body.appendChild(dot);
  }
</script>

<header>
  <h1>Oceanzx Adopt Me Shop</h1>
  <p>Fast delivery • Trusted trades • DM before payment</p>
  <p>All items delivered digitally or in-game</p>
</header>

<div class="container">
  <h2>🌊 Available AM Items 🌊</h2>
  
  <div class="item">
    <span class="item-name">Cerberus Fly Ride</span>
    <span class="item-price">$3</span>
    <a href="https://discord.com/channels/jasonlolololol123df" class="buy-btn" target="_blank">Buy</a>
  </div>

  <div class="item">
    <span class="item-name">Ride Sakura Spirit</span>
    <span class="item-price">$8</span>
    <a href="https://discord.com/channels/jasonlolololol123df" class="buy-btn" target="_blank">Buy</a>
  </div>

  <div class="item">
    <span class="item-name">Neon Sneak Weasel (5)</span>
    <span class="item-price">$12</span>
    <a href="https://discord.com/channels/jasonlolololol123df" class="buy-btn" target="_blank">Buy</a>
  </div>

  <div class="item">
    <span class="item-name">Dango Penguins</span>
    <span class="item-price">$10</span>
    <a href="https://discord.com/channels/jasonlolololol123df" class="buy-btn" target="_blank">Buy</a>
  </div>

  <div class="item">
    <span class="item-name">Axolotl Fly Ride</span>
    <span class="item-price">$2</span>
    <a href="https://discord.com/channels/jasonlolololol123df" class="buy-btn" target="_blank">Buy</a>
  </div>

  <div class="item">
    <span class="item-name">Snow Owl Fly Ride</span>
    <span class="item-price">$2.50</span>
    <a href="https://discord.com/channels/jasonlolololol123df" class="buy-btn" target="_blank">Buy</a>
  </div>

  <p style="text-align:center; margin-top:20px; font-size:0.9rem;">
    📦 Delivery via in-game trade<br>
    📩 DM BEFORE PAYMENT • CASH APP ONLY
  </p>

  <a href="https://www.tiktok.com/@amtrades080" class="tiktok-btn" target="_blank">🌟 Follow me on TikTok 🌟</a>
</div>

<footer>
  -DM ON DISCORD-
</footer>

</body>
</html>

