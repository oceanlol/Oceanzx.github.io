
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
/* General */
body {margin:0; font-family:Arial; background:black; color:#e0e0e0; overflow-x:hidden;}
.dot{position:absolute;background:white;border-radius:50%;opacity:0.8;animation:moveDot linear infinite;}
@keyframes moveDot{0%{transform:translateY(0) translateX(0);}100%{transform:translateY(120vh) translateX(50vw);}}

/* Header */
header{text-align:center;padding:15px;background:#111;border-bottom:2px solid #444;border-radius:0 0 20px 20px;}
header h1{margin:0;color:#f0f0f0;font-size:1.5rem;}
header p{margin:5px 0 0;color:#ccc;font-size:0.85rem;}

/* Container */
.container{max-width:900px;margin:20px auto;padding:15px;background:#1a1a1a;border-radius:20px;box-shadow:0 6px 15px rgba(0,0,0,0.5);}
.section-title{text-align:center;font-size:1.3rem;margin:15px 0;color:#f0f0f0;}

/* Grid */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px;justify-items:center;}
.product-card{text-decoration:none;color:inherit;width:100%;}
.item{background:#222;padding:12px;border-radius:15px;display:flex;flex-direction:column;align-items:center;transition:transform 0.3s,box-shadow 0.3s;}
.item:hover{transform:translateY(-3px);box-shadow:0 5px 12px rgba(255,255,255,0.2);}
.product-img{width:100%;max-width:140px;height:auto;object-fit:cover;border-radius:15px;margin-bottom:8px;}
.item-name{font-weight:bold;font-size:0.95rem;text-align:center;}
.item-price{color:#aaa;font-weight:bold;margin-top:3px;}

/* Buttons */
.buy-btn,.tiktok-btn{background:#333;color:#fff;border:none;padding:6px 12px;border-radius:12px;cursor:pointer;font-weight:bold;text-decoration:none;transition:all 0.3s;margin-top:6px;font-size:0.85rem;}
.buy-btn:hover,.tiktok-btn:hover{background:#555;transform:scale(1.05);}

/* Footer */
footer{text-align:center;padding:12px;margin-top:20px;color:#aaa;font-size:0.85rem;}

/* Responsive tweaks */
@media (max-width:480px){
    header h1{font-size:1.2rem;}
    header p{font-size:0.75rem;}
    .section-title{font-size:1.1rem;}
    .item-name{font-size:0.85rem;}
    .item-price{font-size:0.8rem;}
    .product-img{max-width:120px;}
    .buy-btn,.tiktok-btn{font-size:0.75rem;padding:5px 10px;}
    .container{padding:10px;margin:15px;}
}
</style>
</head>
<body>
<script>
const numDots=80;
for(let i=0;i<numDots;i++){
const dot=document.createElement('div');dot.classList.add('dot');
const size=Math.random()*3+1;dot.style.width=size+'px';dot.style.height=size+'px';
dot.style.top=Math.random()*window.innerHeight+'px';dot.style.left=Math.random()*window.innerWidth+'px';
dot.style.animationDuration=(20+Math.random()*40)+'s';document.body.appendChild(dot);}
</script>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted trades • DM before payment</p>
<p>All items delivered digitally or in-game</p>
</header>

<div class="container">
<div class="section-title">🔥 Most Popular 🔥</div>
<div class="grid">
<a href="ride-sakura-spirit.html" class="product-card"><div class="item"><img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg" class="product-img" alt="Ride Sakura Spirit"><span class="item-name">Ride Sakura Spirit</span><span class="item-price">$8</span></div></a>
<a href="neon-sneak-weasel.html" class="product-card"><div class="item"><img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png" class="product-img" alt="Neon Sneak Weasel"><span class="item-name">Neon Sneak Weasel (5)</span><span class="item-price">$12</span></div></a>
</div>

<div class="section-title">🌊 Available AM Items 🌊</div>
<div class="grid">
<a href="cerberus-fly-ride.html" class="product-card"><div class="item"><img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg" class="product-img" alt="Cerberus Fly Ride"><span class="item-name">Cerberus Fly Ride</span><span class="item-price">$3</span></div></a>
<a href="dango-penguins.html" class="product-card"><div class="item"><img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png" class="product-img" alt="Dango Penguins"><span class="item-name">Dango Penguins</span><span class="item-price">$10</span></div></a>
<a href="axolotl-fly-ride.html" class="product-card"><div class="item"><img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png" class="product-img" alt="Axolotl Fly Ride"><span class="item-name">Axolotl Fly Ride</span><span class="item-price">$2</span></div></a>
<a href="snow-owl-fly-ride.html" class="product-card"><div class="item"><img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg" class="product-img" alt="Snow Owl Fly Ride"><span class="item-name">Snow Owl Fly Ride</span><span class="item-price">$2.50</span></div></a>
</div>

<p style="text-align:center; margin-top:15px; font-size:0.85rem;">📦 Delivery via in-game trade<br>📩 DM BEFORE PAYMENT • CASH APP ONLY</p>
<a href="https://www.tiktok.com/@amtrades080" class="tiktok-btn" target="_blank">🌟 Follow me on TikTok 🌟</a>
</div>

<footer>-DM ON DISCORD-</footer>
</body>
</html>


