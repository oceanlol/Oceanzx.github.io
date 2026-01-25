<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>

<style>
:root{
--accent:#0a84ff;
--gold:#ffd700;
--bg:#0b0b0b;
--card:#1c1c1c;
--text:#ffffff;
}

.light{
--bg:#f4f4f4;
--card:#ffffff;
--text:#000000;
}

*{box-sizing:border-box}

body{
margin:0;
font-family:Segoe UI,Arial,sans-serif;
background:var(--bg);
color:var(--text);
overflow-x:hidden;
transition:.3s;
}

/* PARTICLES */
.dot{
position:fixed;
width:3px;height:3px;
background:white;
border-radius:50%;
opacity:.5;
animation:float linear infinite;
}
@keyframes float{
from{transform:translateY(-10vh)}
to{transform:translateY(120vh)}
}

/* HEADER */
header{
text-align:center;
padding:40px 20px;
background:linear-gradient(180deg,#111,#000);
border-bottom:1px solid #222;
}
header h1{margin:0;font-size:2.3rem}
header p{color:#aaa}

/* TOGGLES */
.top-btns{
position:fixed;
top:15px;left:15px;
display:flex;gap:10px;
z-index:999;
}
.toggle{
padding:8px 14px;
border-radius:14px;
border:none;
background:var(--accent);
color:white;
cursor:pointer;
}

/* CONTAINER */
.container{
max-width:1200px;
margin:30px auto;
padding:25px;
background:var(--card);
border-radius:30px;
box-shadow:0 0 50px rgba(10,132,255,.15);
}

/* GRID */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
gap:28px;
}

/* CARD */
.card{
background:linear-gradient(180deg,#1e1e1e,#121212);
border-radius:28px;
padding:18px;
text-align:center;
cursor:pointer;
transition:.35s;
position:relative;
}
.card:hover{
transform:translateY(-8px) scale(1.02);
box-shadow:0 0 35px rgba(10,132,255,.4);
}
.card img{
width:150px;height:150px;
object-fit:cover;
border-radius:22px;
}

.popular{
border:2px solid gold;
box-shadow:0 0 30px rgba(255,215,0,.7);
}
.badge{
position:absolute;
top:12px;left:12px;
background:linear-gradient(180deg,#ffd700,#ffae00);
color:black;
padding:6px 12px;
border-radius:14px;
font-size:.75rem;
font-weight:bold;
}

/* BUTTON */
.btn{
background:linear-gradient(180deg,var(--accent),#0066cc);
border:none;
padding:10px 20px;
border-radius:18px;
color:white;
font-weight:bold;
cursor:pointer;
transition:.3s;
}
.btn:hover{transform:scale(1.08)}

/* CART */
#cart{
position:fixed;
top:20px;right:20px;
background:var(--card);
border-radius:24px;
padding:18px;
width:280px;
box-shadow:0 0 35px rgba(0,0,0,.8);
}
.cart-item{
display:flex;
justify-content:space-between;
margin:6px 0;
font-size:.9rem;
}

/* MODAL */
#modal{
display:none;
position:fixed;
top:0;left:0;
width:100vw;height:100vh;
background:rgba(0,0,0,.95);
z-index:1000;
justify-content:center;
align-items:center;
}
.modal-box{
background:#1a1a1a;
padding:30px;
border-radius:30px;
text-align:center;
max-width:350px;
}

/* LIVE POPUP */
#live{
position:fixed;
bottom:20px;left:20px;
background:#111;
padding:12px 18px;
border-radius:18px;
font-size:.85rem;
box-shadow:0 0 20px rgba(10,132,255,.4);
display:none;
}

/* MOBILE */
@media(max-width:600px){
#cart{width:240px}
}
</style>
</head>

<body>

<div class="top-btns">
<button class="toggle" onclick="toggleMode()">🌗</button>
</div>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="container">
<h2 style="text-align:center">⭐ Most Popular ⭐</h2>
<div class="grid">
<div class="card popular" onclick="openModal('Cerberus Fly Ride',3)">
<div class="badge">HOT</div>
<img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg">
<h3>Cerberus Fly Ride</h3>
<p>$3</p>
</div>
</div>

<h2 style="text-align:center;margin-top:40px">🔥 Available Pets 🔥</h2>
<div class="grid">
<div class="card" onclick="openModal('Axolotl Fly Ride',2)">
<img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png">
<h3>Axolotl Fly Ride</h3><p>$2</p>
</div>
<div class="card" onclick="openModal('Snow Owl Fly Ride',2.5)">
<img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg">
<h3>Snow Owl Fly Ride</h3><p>$2.50</p>
</div>
</div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<b>Total: $<span id="total">0</span></b>
<br><br>
<button class="btn" onclick="checkout()">Checkout</button>
</div>

<div id="modal">
<div class="modal-box">
<h2 id="m-name"></h2>
<h3>$<span id="m-price"></span></h3>
<button class="btn" onclick="addToCart()">Add to Cart</button>
<br><br>
<button class="btn" onclick="closeModal()">Close</button>
</div>
</div>

<div id="live"></div>

<script>
let cart=[],current={};

function openModal(n,p){
current={name:n,price:p};
document.getElementById("m-name").innerText=n;
document.getElementById("m-price").innerText=p;
modal.style.display="flex";
}
function closeModal(){modal.style.display="none"}

function addToCart(){
cart.push(current);
renderCart();
closeModal();
}

function renderCart(){
let total=0;
cart-items.innerHTML="";
cart.forEach(i=>{
total+=i.price;
cart-items.innerHTML+=`<div class="cart-item"><span>${i.name}</span><span>$${i.price}</span></div>`;
});
document.getElementById("total").innerText=total.toFixed(2);
}

function checkout(){
let text="Oceanzx Order:\n";
let total=0;
cart.forEach(i=>{text+=`- ${i.name} $${i.price}\n`;total+=i.price});
text+=`Total: $${total}`;
navigator.clipboard.writeText(text);
window.open("https://discord.com/users/1455058787257024512","_blank");
}

function toggleMode(){
document.body.classList.toggle("light");
}

// LIVE POPUP
const buyers=["Axolotl","Cerberus","Snow Owl","Neon Pet"];
setInterval(()=>{
const l=document.getElementById("live");
l.innerText=`Someone just bought ${buyers[Math.floor(Math.random()*buyers.length)]}!`;
l.style.display="block";
setTimeout(()=>l.style.display="none",4000);
},9000);

// particles
for(let i=0;i<90;i++){
let d=document.createElement("div");
d.className="dot";
d.style.left=Math.random()*100+"vw";
d.style.animationDuration=(8+Math.random()*20)+"s";
document.body.appendChild(d);
}
</script>

</body>
</html>
