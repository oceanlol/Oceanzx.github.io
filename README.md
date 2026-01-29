<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Oceanzx Shop</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root{
  --bg:#0b0b0b;
  --card:#141414;
  --text:#ffffff;
  --muted:#bdbdbd;
  --accent:#ffffff;
}

*{box-sizing:border-box}

body{
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:radial-gradient(circle at top, #1a1a1a 0%, #000 70%);
  color:var(--text);
}

/* FAST WHITE DOTS BACKGROUND */
body::before{
  content:"";
  position:fixed;
  inset:0;
  background-image:
    radial-gradient(2px 2px at 20px 30px, #fff 40%, transparent 41%),
    radial-gradient(2px 2px at 100px 80px, #fff 40%, transparent 41%),
    radial-gradient(2px 2px at 200px 150px, #fff 40%, transparent 41%);
  background-size:200px 200px;
  animation:dots 3s linear infinite;
  opacity:.35;
  pointer-events:none;
}
@keyframes dots{
  from{background-position:0 0}
  to{background-position:-200px -200px}
}

/* TOP BAR */
.top-banner{
  background:#000;
  border-bottom:1px solid #222;
  text-align:center;
  padding:10px;
  font-weight:700;
}

/* HEADER */
header{
  position:sticky;
  top:0;
  z-index:10;
  background:#000;
  padding:14px 18px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  border-bottom:1px solid #222;
}

header h1{
  margin:0;
  font-size:20px;
}

.cart{
  background:#1c1c1c;
  padding:8px 14px;
  border-radius:14px;
  font-size:14px;
  cursor:pointer;
}

/* SECTIONS */
section{
  padding:24px;
}

section h2{
  margin:0 0 14px;
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(200px,1fr));
  gap:16px;
}

/* CARD */
.card{
  background:var(--card);
  border-radius:18px;
  padding:14px;
  text-align:center;
}

.card img{
  width:100%;
  height:160px;
  object-fit:contain;
  border-radius:16px;
}

.card h3{
  font-size:14px;
  margin:10px 0 6px;
}

.price{
  font-weight:700;
}

.stock{
  font-size:12px;
  color:var(--muted);
}

button{
  margin-top:8px;
  width:100%;
  padding:8px;
  border-radius:12px;
  border:none;
  background:#fff;
  color:#000;
  font-weight:700;
  cursor:pointer;
}

/* FOOTER */
footer{
  padding:24px;
  text-align:center;
  color:var(--muted);
}

footer a{
  color:#fff;
  text-decoration:none;
  font-weight:700;
}
</style>
</head>

<body>

<div class="top-banner">
$10 OFF $45 ORDERS • Ends on FEB 1st
</div>

<header>
  <h1>Oceanzx Shop</h1>
  <div class="cart">🛒 Cart (<span id="cartCount">0</span>)</div>
</header>

<section>
<h2>🔥 Featured Deal</h2>
<div class="grid">
  <div class="card">
    <img src="https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png">
    <h3>10x Royal Egg</h3>
    <div class="price">$7</div>
    <div class="stock">Limited</div>
    <button onclick="add()">Add to Cart</button>
  </div>
</div>
</section>

<section>
<h2>🐶 Pets</h2>
<div class="grid" id="pets"></div>
</section>

<section>
<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>
</section>

<footer>
Checkout via Discord →  
<a href="https://discord.gg/sv6tRJBR5G" target="_blank">discord.gg/sv6tRJBR5G</a>
</footer>

<script>
let cart=0;
function add(){
  cart++;
  document.getElementById("cartCount").innerText=cart;
}

const pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:4},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:4},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:3},
{name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg",stock:4},
{name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",stock:5},
{name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",stock:5},
{name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",stock:5},
{name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:4},
{name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png",stock:5},
{name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:5},
{name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769571888116-fe636100-1ac8-4c9c-aaeb-0bfd97d9adb1.jpg",stock:5},
{name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769571952502-156e70c2-979b-4008-a84e-d3dbab31f72d.webp",stock:5},
{name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769572019588-bb64eee7-b0d3-40cc-9fa6-8a09e3dc8a51.jpg",stock:5}
];

const eggs=[
{name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png",stock:15},
{name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png",stock:15},
{name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png",stock:15},
{name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15}
];

function render(list,id){
  document.getElementById(id).innerHTML=list.map(i=>`
  <div class="card">
    <img src="${i.img}">
    <h3>${i.name}</h3>
    <div class="price">$${i.price}</div>
    <div class="stock">Stock: ${i.stock}</div>
    <button onclick="add()">Add to Cart</button>
  </div>`).join("");
}

render(pets,"pets");
render(eggs,"eggs");
</script>

</body>
</html>
