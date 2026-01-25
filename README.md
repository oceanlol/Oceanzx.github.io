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
    background: linear-gradient(to bottom, #cce7ff, #f0f8ff);
    color: #333;
    overflow-x: hidden;
  }

  /* Floating clouds */
  .cloud {
    position: absolute;
    background: rgba(255,255,255,0.8);
    border-radius: 50%;
    opacity: 0.8;
    animation: floatClouds linear infinite;
  }

  /* Different sizes and speeds for depth */
  .cloud.layer1 { width: 120px; height: 60px; top: 50px; left: -150px; animation-duration: 70s; }
  .cloud.layer2 { width: 200px; height: 80px; top: 150px; left: -250px; animation-duration: 90s; }
  .cloud.layer3 { width: 150px; height: 70px; top: 250px; left: -200px; animation-duration: 80s; }
  .cloud.layer4 { width: 180px; height: 90px; top: 320px; left: -220px; animation-duration: 100s; }

  @keyframes floatClouds {
    0% { transform: translateX(0); }
    100% { transform: translateX(120vw); }
  }

  header {
    text-align: center;
    padding: 20px;
    background: rgba(255, 255, 255, 0.5);
    backdrop-filter: blur(10px);
    border-bottom: 2px solid #00aaff;
    position: relative;
    z-index: 2;
  }
  header h1 {
    margin: 0;
    color: #005f99;
    text-shadow: 1px 1px 5px #a0d8ff;
  }
  header p {
    margin: 5px 0 0;
    font-size: 0.9rem;
    color: #0077cc;
  }

  .container {
    max-width: 700px;
    margin: 30px auto;
    padding: 20px;
    background: rgba(255,255,255,0.6);
    border-radius: 20px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.1);
    position: relative;
    z-index: 2;
  }

  h2 {
    text-align: center;
    color: #0077cc;
    text-shadow: 1px 1px 3px #a0d8ff;
  }

  .item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: rgba(255,255,255,0.8);
    margin: 10px 0;
    padding: 12px 20px;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.05);
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .item:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 15px rgba(0,0,0,0.1);
  }

  .item-name { font-weight: bold; font-size: 1rem; }
  .item-price { color: #005f99; font-weight: bold; margin-right: 15px; }

  .buy-btn, .tiktok-btn {
    background: linear-gradient(90deg, #00cfff, #0077cc);
    color: white;
    border: none;
    padding: 8px 14px;
    border-radius: 10px;
    cursor: pointer;
    font-weight: bold;
    text-decoration: none;
    box-shadow: 0 0 8px #00cfff, 0 0 15px #0077cc;
    transition: all 0.3s;
  }
  .buy-btn:hover, .tiktok-btn:hover {
    box-shadow: 0 0 15px #00e0ff, 0 0 25px #0099ff;
    transform: scale(1.05);
  }

  .tiktok-btn { display: inline-block; margin: 20px auto; text-align: center; }

  footer {
    text-align: center;
    padding: 15px;
    margin-top: 30px;
    color: #005f99;
    font-size: 0.9rem;
    position: relative;
    z-index: 2;
  }
</style>
</head>
<body>

<!-- Clouds -->
<div class="cloud layer1"></div>
<div class="cloud layer2"></div>
<div class="cloud layer3"></div>
<div class="cloud layer4"></div>

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

