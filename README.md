<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OCEANZX — Adopt Me Shop</title>
<meta name="viewport" content="width=1200">
<meta name="description" content="OCEANZX Adopt Me Shop — Clean • Trusted • Instant Checkout">

<style>
/* ===== ROOT ===== */
:root{
--bg:#0a0a0a;
--card:#111;
--border:#1f1f1f;
--text:#fff;
--muted:#9a9a9a;
--accent:#fff;
--soft:#161616;
}

*{box-sizing:border-box}
body{
margin:0;
background:var(--bg);
color:var(--text);
font-family:Inter,Segoe UI,Arial,sans-serif;
}

/* ===== HEADER ===== */
header{
text-align:center;
padding:50px 20px 30px;
border-bottom:1px solid var(--border);
}
header h1{
margin:0;
font-size:48px;
letter-spacing:4px;
}
header p{
margin-top:10px;
color:var(--muted);
}

/* ===== VIEWERS ===== */
.viewers{
position:fixed;
top:20px;
left:20px;
background:var(--card);
border:1px solid var(--border);
padding:10px 14px;
border-radius:14px;
font-size:14px;
}

/* ===== CONTAINER ===== */
.container{
max-width:1200px;
margin:40px auto;
padding:0 20px;
}

/* ===== SECTION ===== */
.section-title{
font-size:28px;
margin-bottom:18px;
border-left:4px solid white;
padding-left:12px;
}

/* ===== GRID ===== */
.grid{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:24px;
}

/* ===== CARD ===== */
.card{
background:var(--card);
border:1px solid var(--border);
border-radius:22px;
padding:18px;
transition:.25s;
}
.card:hover{
transform:translateY(-4px);
border-color:white;
}
.card img{
width:100%;
height:180px;
object-fit:contain;
border-radius:14px;
background:#000;
}
.card h3{
margin:14px 0 6px;
font-size:18px;
}
.card .price{
font-weight:bold;
}
.card button{
margin-top:12px;
width:100%;
padding:12px;
border-radius:14px;
border:none;
background:white;
color:black;
font-weight:bold;
cursor:pointer;
}

/* ===== CART ===== */
#cart{
position:fixed;
top:100px;
right:20px;
width:340px;
background:var(--soft);
border:1px solid var(--border);
border-radius:24px;
padding:16px;
}
#cart h2{
margin:0 0 10px;
text-align:center;
}
.cart-item{
display:flex;
gap:10px;
align-items:center;
margin:10px 0;
}
.cart-item img{
width:50px;
height:50px;
object-fit:contain;
background:black;
border-radius:10px;
}
.cart-item span{
font-size:14px;
}
.cart-total{
margin-top:12px;
font-weight:bold;
text-align:center;
}
.cart-btn{
margin-top:10px;
width:100%;
padding:12px;
border-radius:14px;
background:white;
color:black;
border:none;
font-weight:bold;
cursor:pointer;
}

/* ===== MODAL ===== */
#checkoutModal{
position:fixed;
inset:0;
background:rgba(0,0,0,.85);
display:none;
align-items:center;
justify-content:center;
z-index:9999;
}
.modal-box{
background:#111;
border-radius:26px;
padding:26px;
width:500px;
text-align:center;
}
.modal-box h3{margin-top:0}
.modal-box pre{
background:black;
padding:14px;
border-radius:14px;
text-align:left;
max-height:240px;
overflow:auto;
}

/* ===== DEV BUTTON ===== */
#devBtn{
position:fixed;
right:10px;
bottom:10px;
width:44px;
height:44px;
border-radius:50%;
background:white;
color:black;
font-weight:bold;
display:flex;
align-items:center;
justify-content:center;
cursor:pointer;
}

/* ===== UPDATES ===== */
#updates{
position:fixed;
left:20px;
bottom:20px;
background:var(--card);
border:1px solid var(--border);
padding:14px;
border-radius:18px;
width:260px;
}
</style>
</head>

<body>

<header>
<h1>OCEANZX</h1>
<p>Adopt Me • Clean • Trusted</p>
</header>

<div class="viewers">👀 <span id="viewerCount"></span> people viewing</div>

<div class="container">

<h2 class="section-title">🥚 Eggs</h2>
<div class="grid" id="eggs"></div>

<h2 class="section-title">🐾 Pets</h2>
<div class="grid" id="pets"></div>

</div>

<!-- CART -->
<div id="cart">
<h2>🛒 Cart</h2>
<div id="cartItems"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="cart-btn" onclick="openCheckout()">Checkout</button>
</div>

<!-- CHECKOUT -->
<div id="checkoutModal">
<div class="modal-box">
<h3>Screenshot this 🧾</h3>
<p>Send this screenshot in the Discord ticket</p>
<pre id="receipt"></pre>
<p><b>Cash App:</b> $Bananaboy723</p>
<button class="cart-btn" onclick="finish()">Go to Discord</button>
</div>
</div>

<!-- UPDATES -->
<div id="updates">
<b>📢 Updates</b>
<ul>
<li>New clean UI</li>
<li>Discount codes</li>
<li>Dev mode added</li>
</ul>
</div>

<div id="devBtn" onclick="dev()">O</div>

<audio id="ding" src="https://assets.mixkit.co/sfx/preview/mixkit-click-melodic-tone-1129.mp3"></audio>

<script>
/* ===== DATA ===== */
const eggs=[
{name:"Crystal Egg",price:1,img:"https://starpets.gg/adopt-me/shop/egg/crystal_egg/151744"},
{name:"Retired Egg (2)",price:1,img:"https://starpets.gg/adopt-me/shop/egg/retired_egg/28325"},
{name:"Moon Egg (2)",price:1.25,img:"https://starpets.gg/adopt-me/shop/egg/moon_egg/31568"},
{name:"Royal Egg (5)",price:1,img:"https://starpets.gg/adopt-me/shop/egg/royal_egg/28311"},
{name:"Aussie Egg (2)",price:10,img:"https://starpets.gg/adopt-me/shop/egg/aussie_egg/28315"}
];

const pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:35,img:"https://image2url.com/r2/default/images/1769417417556-2117c23b-fadc-4197-9aca-9023736ecf7a.png"},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417494592-7c9b625a-9528-459c-bdae-ec45773ce972.png"},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"},
{name:"Dragonfruit Fox",price:10,img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png"},
{name:"Unicorn",price:3,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
{name:"German Shepherd Fly Ride",price:10,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"},
{name:"Turtle Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"}
];

let cart=[];

/* ===== RENDER ===== */
function render(list,id){
const el=document.getElementById(id);
list.forEach(i=>{
el.innerHTML+=`
<div class="card">
<img src="${i.img}">
<h3>${i.name}</h3>
<div class="price">$${i.price}</div>
<button onclick='add(${JSON.stringify(i)})'>Add to Cart</button>
</div>`;
});
}
render(eggs,"eggs");
render(pets,"pets");

/* ===== CART ===== */
function add(i){
document.getElementById("ding").play();
cart.push(i);
updateCart();
}
function updateCart(){
const c=document.getElementById("cartItems");
c.innerHTML="";
let t=0;
cart.forEach(i=>{
t+=i.price;
c.innerHTML+=`
<div class="cart-item">
<img src="${i.img}">
<span>${i.name}</span>
<span>$${i.price}</span>
</div>`;
});
document.getElementById("total").innerText=t.toFixed(2);
}

/* ===== CHECKOUT ===== */
function openCheckout(){
if(!cart.length)return;
const id=Math.floor(Math.random()*900000+100000);
let txt=`Order ID: ${id}\n\n`;
let t=0;
cart.forEach(i=>{txt+=`• ${i.name} - $${i.price}\n`;t+=i.price});
txt+=`\nTotal: $${t}`;
document.getElementById("receipt").innerText=txt;
navigator.clipboard.writeText(txt);
document.getElementById("checkoutModal").style.display="flex";
}
function finish(){
window.location.href="https://discord.gg/sv6tRJBR5G";
}

/* ===== VIEWERS ===== */
document.getElementById("viewerCount").innerText=Math.floor(Math.random()*20+15);

/* ===== DEV ===== */
function dev(){
const p=prompt("Password");
if(p==="Keebs"){
const msg=prompt("Admin message to show:");
if(msg)alert("ADMIN: "+msg);
}
}
</script>

</body>
</html>
