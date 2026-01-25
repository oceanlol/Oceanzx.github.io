<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: black;
  color: #e0e0e0;
  overflow-x: hidden;
  position: relative;
}
.dot {
  position: absolute;
  border-radius: 50%;
  background: white;
  opacity: 0.8;
  animation: moveDot linear infinite;
}
@keyframes moveDot {
  0% { transform: translateY(0) translateX(0); }
  100% { transform: translateY(120vh) translateX(50vw); }
}

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

.buy-btn {
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

.buy-btn:hover {
  background: #555;
  transform: scale(1.05);
}

footer {
  text-align: center;
  padding: 12px;
  margin-top: 20px;
  color: #aaa;
  font-size: 0.85rem;
}

@media (max-width:480px){
  header h1{font-size:1.2rem;}
  header p{font-size:0.75rem;}
  .section-title{font-size:1.1rem;}
  .item-name{font-size:0.85rem;}
  .item-price{font-size:0.8rem;}
  .product-img{max-width:120px;height:120px;}
  .buy-btn{font-size:0.75rem;padding:5px 10px;}
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
  <div class="section-title">🔥 Available Pets 🔥</div>
  <div class="grid">
    <a class="product-card" href="https://discord.com/channels/jasonlolololol123df" target="_blank">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png" class="product-img" alt="Axolotl Fly Ride">
        <div class="item-name">Axolotl Fly Ride</div>
        <div class="item-price">$2</div>
        <div class="buy-btn">Buy Now</div>
      </div>
    </a>

    <a class="product-card" href="https://discord.com/channels/jasonlolololol123df" target="_blank">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg" class="product-img" alt="Cerberus Fly Ride">
        <div class="item-name">Cerberus Fly Ride</div>
        <div class="item-price">$3</div>
        <div class="buy-btn">Buy Now</div>
      </div>
    </a>

    <a class="product-card" href="https://discord.com/channels/jasonlolololol123df" target="_blank">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png" class="product-img" alt="Dango Penguins">
        <div class="item-name">Dango Penguins</div>
        <div class="item-price">$10</div>
        <div class="buy-btn">Buy Now</div>
      </div>
    </a>

    <a class="product-card" href="https://discord.com/channels/jasonlolololol123df" target="_blank">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png" class="product-img" alt="Neon Sneak Weasel">
        <div class="item-name">Neon Sneak Weasel (5)</div>
        <div class="item-price">$12</div>
        <div class="buy-btn">Buy Now</div>
      </div>
    </a>

    <a class="product-card" href="https://discord.com/channels/jasonlolololol123df" target="_blank">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg" class="product-img" alt="Ride Sakura Spirit">
        <div class="item-name">Ride Sakura Spirit</div>
        <div class="item-price">$8</div>
        <div class="buy-btn">Buy Now</div>
      </div>
    </a>

    <a class="product-card" href="https://discord.com/channels/jasonlolololol123df" target="_blank">
      <div class="item">
        <img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg" class="product-img" alt="Snow Owl Fly Ride">
        <div class="item-name">Snow Owl Fly Ride</div>
        <div class="item-price">$2.50</div>
        <div class="buy-btn">Buy Now</div>
      </div>
    </a>
  </div>

  <p style="text-align:center; margin-top:20px;">
    🌟 DM me on Discord 🌟<br>
    <a class="buy-btn" href="https://discord.gg/sv6tRJBR5G" target="_blank">Join Discord</a>
  </p>
</div>

<footer>
  &copy; 2026 Oceanzx Adopt Me Shop
</footer>

<script>
// Moving dots background
const numDots = 100;
for(let i = 0; i < numDots; i++) {
  const dot = document.createElement('div');
  dot.classList.add('dot');
  const size = Math.random()*3+1;
  dot.style.width = dot.style.height = size+'px';
  dot.style.top = Math.random()*window.innerHeight+'px';
  dot.style.left = Math.random()*window.innerWidth+'px';
  dot.style.animationDuration = (20+Math.random()*40)+'s';
  document.body.appendChild(dot);
}
</script>

</body>
</html>
