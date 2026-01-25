
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
    overflow-x: hidden;
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
    border-radius: 0 0 25px 25px;
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
    max-width: 900px;
    margin: 30px auto;
    padding: 20px;
    background: #1a1a1a;
    border-radius: 25px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.5);
    position: relative;
    z-index: 2;
  }

  h2 {
    text-align: center;
    color: #f0f0f0;
    margin-bottom: 20px;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 20px;
  }

  .product-card {
    display: block;
    text-decoration: none;
    color: inherit;
  }

  .item {
    background: #222;
    padding: 15px;
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .item:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 15px rgba(255,255,255,0.2);
  }

  .product-img {
    width: 120px;
    height: 120px;
    object-fit: cover;
    border-radius: 20px;
    margin-bottom: 10px;
  }

  .item-name { font-weight: bold; font-size: 1rem; text-align: center; }
  .item-price { color: #aaa; font-weight: bold; margin-top: 5px; }

  .buy-btn, .tiktok-btn {
    background: #333;
    color: #fff;
    border: none;
    padding: 8px 14px;
    border-radius: 15px;
    cursor: pointer;
    font-weight: bold;
    text-decoration: none;
    transition: all 0.3s;
    margin-top: 10px;
  }
  .buy-btn:hover, .tiktok-btn:hover {
    background: #555;
    transform: scale(1.05);
  }

  .section-title {
    text-align: center;
    font-size: 1.3rem;
    margin: 20px 0;
    color: #f0f0f0;
  }

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
  const numDots = 100;
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
  <!-- Most Popular Section -->
  <div class="section-title">🔥 Most Popular 🔥</div>
  <div class="grid">
    <a href="ride-sakura-spirit.html" class="product-card">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg" class="product-img" alt="Ride Sakura Spirit">
        <span class="item-name">Ride Sakura Spirit</span>
        <span class="item-price">$8</span>
      </div>
    </a>

    <a href="neon-sneak-weasel.html" class="product-card">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png" class="product-img" alt="Neon Sneak Weasel">
        <span class="item-name">Neon Sneak Weasel (5)</span>
        <span class="item-price">$12</span>
      </div>
    </a>
  </div>

  <!-- All Other Items -->
  <div class="section-title">🌊 Available AM Items 🌊</div>
  <div class="grid">
    <a href="cerberus-fly-ride.html" class="product-card">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg" class="product-img" alt="Cerberus Fly Ride">
        <span class="item-name">Cerberus Fly Ride</span>
        <span class="item-price">$3</span>
      </div>
    </a>

    <a href="dango-penguins.html" class="product-card">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png" class="product-img" alt="Dango Penguins">
        <span class="item-name">Dango Penguins</span>
        <span class="item-price">$10</span>
      </div>
    </a>

    <a href="axolotl-fly-ride.html" class="product-card">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png" class="product-img" alt="Axolotl Fly Ride">
        <span class="item-name">Axolotl Fly Ride</span>
        <span class="item-price">$2</span>
      </div>
    </a>

    <a href="snow-owl-fly-ride.html" class="product-card">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg" class="product-img" alt="Snow Owl Fly Ride">
        <span class="item-name">Snow Owl Fly Ride</span>
        <span class="item-price">$2.50</span>
      </div>
    </a>
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


</body>
</html>

