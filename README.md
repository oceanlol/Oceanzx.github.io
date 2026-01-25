<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
  /* General */
  body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: black;
    color: #e0e0e0;
    overflow-x: hidden;
    position: relative;
    cursor: crosshair;
  }

  .dot {
    position: absolute;
    width: 6px;
    height: 6px;
    background: white;
    border-radius: 50%;
    opacity: 0.8;
    animation: moveDot linear infinite;
  }

  @keyframes moveDot {
    0% { transform: translateY(0) translateX(0); }
    100% { transform: translateY(120vh) translateX(50vw); }
  }

  /* Header */
  header {
    text-align: center;
    padding: 15px;
    background: #111;
    border-bottom: 2px solid #444;
    border-radius: 0 0 20px 20px;
  }

  header h1 {
    margin: 0;
    color: #f0f0f0;
    font-size: 1.5rem;
  }

  header p {
    margin: 5px 0 0;
    color: #ccc;
    font-size: 0.85rem;
  }

  /* Container */
  .container {
    max-width: 900px;
    margin: 20px auto;
    padding: 15px;
    background: #1a1a1a;
    border-radius: 20px;
    box-shadow: 0 6px 15px rgba(0,0,0,0.5);
  }

  .section-title {
    text-align: center;
    font-size: 1.3rem;
    margin: 15px 0;
    color: #f0f0f0;
  }

  /* Grid */
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 15px;
    justify-items: center;
  }

  .product-card {
    text-decoration: none;
    color: inherit;
    width: 100%;
  }

  .item {
    background: #222;
    padding: 12px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .item:hover {
    transform: translateY(-3px);
    box-shadow: 0 5px 12px rgba(255,255,255,0.2);
  }

  .product-img {
    width: 100%;
    max-width: 140px;
    height: 140px;
    object-fit: cover;
    border-radius: 15px;
    margin-bottom: 8px;
  }

  .item-name {
    font-weight: bold;
    font-size: 0.95rem;
    text-align: center;
  }

  .item-price {
    color: #aaa;
    font-weight: bold;
    margin-top: 3px;
  }

  /* Buttons */
  .buy-btn, .tiktok-btn {
    background: #333;
    color: #fff;
    border: none;
    padding: 6px 12px;
    border-radius: 12px;
    cursor: pointer;
    font-weight: bold;
    text-decoration: none;
    transition: all 0.3s;
    margin-top: 6px;
    font-size: 0.85rem;
  }

  .buy-btn:hover, .tiktok-btn:hover {
    background: #555;
    transform: scale(1.05);
  }

  /* Footer */
  footer {
    text-align: center;
    padding: 12px;
    margin-top: 20px;
    color: #aaa;
    font-size: 0.85rem;
  }

  /* Responsive tweaks */
  @media (max-width:480px){
    header h1{font-size:1.2rem;}
    header p{font-size:0.75rem;}
    .section-title{font-size:1.1rem;}
    .item-name{font-size:0.85rem;}
    .item-price{font-size:0.8rem;}
    .product-img{max-width:120px;height:120px;}
    .buy-btn,.tiktok-btn{font-size:0.75rem;padding:5px 10px;}
    .container{padding:10px;margin:15px;}
  }
</style>
</head>
<body>

<header>
  <h1>Oceanzx Adopt Me Shop</h1>
  <p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="container">
  <p style="text-align:center;">All items delivered digitally or in-game</p>

  <div class="section-title">🔥 Most Popular 🔥</div>
  <div class="grid">
    <a class="product-card" href="#">
      <div class="item">
        <img class="product-img" src="https://via.placeholder.com/140" alt="Ride Sakura Spirit">
        <div class="item-name">Ride Sakura Spirit</div>
        <div class="item-price">$8</div>
        <button class="buy-btn">Buy</button>
      </div>
    </a>

    <a class="product-card" href="#">
      <div class="item">
        <img class="product-img" src="https://via.placeholder.com/140" alt="Neon Sneak Weasel (5)">
        <div class="item-name">Neon Sneak Weasel (5)</div>
        <div class="item-price">$12</div>
        <button class="buy-btn">Buy</button>
      </div>
    </a>
  </div>

  <div class="section-title">🌊 Available AM Items 🌊</div>
  <div class="grid">
    <a class="product-card" href="#">
      <div class="item">
        <img class="product-img" src="https://via.placeholder.com/140" alt="Cerberus Fly Ride">
        <div class="item-name">Cerberus Fly Ride</div>
        <div class="item-price">$3</div>
        <button class="buy-btn">Buy</button>
      </div>
    </a>

    <a class="product-card" href="#">
      <div class="item">
        <img class="product-img" src="https://via.placeholder.com/140" alt="Dango Penguins">
        <div class="item-name">Dango Penguins</div>
        <div class="item-price">$10</div>
        <button class="buy-btn">Buy</button>
      </div>
    </a>

    <a class="product-card" href="#">
      <div class="item">
        <img class="product-img" src="https://via.placeholder.com/140" alt="Axolotl Fly Ride">
        <div class="item-name">Axolotl Fly Ride</div>
        <div class="item-price">$2</div>
        <button class="buy-btn">Buy</button>
      </div>
    </a>

    <a class="product-card" href="#">
      <div class="item">
        <img class="product-img" src="https://via.placeholder.com/140" alt="Snow Owl Fly Ride">
        <div class="item-name">Snow Owl Fly Ride</div>
        <div class="item-price">$2.50</div>
        <button class="buy-btn">Buy</button>
      </div>
    </a>
  </div>

  <p style="text-align:center;">📦 Delivery via in-game trade<br>📩 DM BEFORE PAYMENT • CASH APP ONLY</p>
  <p style="text-align:center;">🌟 DM me on Discord 🌟<br>
    <a class="tiktok-btn" href="https://discord.gg/sv6tRJBR5G" target="_blank">Join Discord</a>
  </p>
</div>

<footer>
  &copy; 2026 Oceanzx Adopt Me Shop
</footer>

<script>
  // Create interactive animated dots
  const numDots = 80;
  const dots = [];
  for(let i = 0; i < numDots; i++) {
    const dot = document.createElement('div');
    dot.classList.add('dot');
    dot.style.left = Math.random() * 100 + 'vw';
    dot.style.top = Math.random() * 100 + 'vh';
    dot.style.width = dot.style.height = Math.random() * 6 + 4 + 'px';
    dot.style.animationDuration = Math.random() * 5 + 5 + 's';
    document.body.appendChild(dot);
    dots.push(dot);
  }

  // Mouse movement interaction
  document.addEventListener('mousemove', (e) => {
    const moveX = (e.clientX / window.innerWidth - 0.5) * 50;
    const moveY = (e.clientY / window.innerHeight - 0.5) * 50;
    dots.forEach((dot, index) => {
      dot.style.transform = `translate(${moveX/(index+1)}px, ${moveY/(index+1)}px)`;
    });
  });
</script>

</body>
</html>
