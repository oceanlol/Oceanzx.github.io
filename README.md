<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>

<meta name="description" content="Oceanzx Adopt Me Shop – Fast delivery, trusted trades, instant Discord checkout.">

<style>
:root{
--accent:#0a84ff;
--gold:#ffd700;
--bg:#0b0b0b;
--card:#1c1c1c;
--text:#ffffff;
}

*{box-sizing:border-box}

body{
margin:0;
font-family:Segoe UI,Arial,sans-serif;
background:var(--bg);
color:var(--text);
overflow-x:hidden;
}

/* particles */
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

/* header */
header{
text-align:center;
padding:40px 20px;
background:linear-gradient(180deg,#111,#000);
border-bottom:1px solid #222;
}
header h1{margin:0;font-size:2.3rem}
header p{color:#aaa}

/* trust bar */
.trust{
background:#0a84ff;
text-align:center;
padding:10px;
font-weight:bold;
}

/* container */
.container{
max-width:1200px;
margin:30px auto;
padding:25px;
background:#121212;
border-radius:30px;
box-shadow:0 0 50px rgba(10,132,255,.15);
}

/* grid */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
gap:28px;
}

/* card */
.card{
background:linear-gradient(180deg,var(--card),#121212);
border-radius:28px;
padding:18px;
text-align:center;
transition:.35s;
position:relative;
}
.card:hover{
transform:translateY(-6px);
box-shadow:0 0 30px rgba(10,132,255,.4);
}
.card img{
width:150px;height:150px;
object-fit:cover;
border-radius:22px;
}
.price{color:#ccc;font-weight:bold}

.stock{
color:#ff4d4d;
font-size:.8rem;
animation:pulse 1.3s infinite;
}
@keyframes pulse{
0%,100%{opacity:1}
50%{opacity:.5}
}

/* button */
.btn{
background:linear-gradient(180deg,var(--accent),#0066cc);
border:none;
padding:10px 20px;
border-radius:18px;
color:white;
font-weight:bold;
cursor:pointer;
margin-top:8px;
}
.btn:hover{transform:scale(1.05)}

/* cart */
#cart{
position:fixed;
top:20px;right:20px;
background:#121212;
border-radius:24px;
padding:16px;
width:280px;
box-shadow:0 0 30px rgba(0,0,0,.8);
}
.cart-item{
display:flex;
justify-content:space-between;
margin:6px 0;
font-size:.9rem;
}
.cart-total{margin-top:10px;font-weight:bold}

/* mobile */
@media(max-width:600px){
#cart{width:240px}
}
</style>
</head>

<body>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="trust">✔ Instant Delivery • ✔ Trusted Trades • ✔ Discord Support</div>

<div class="container">

<h2 style="text-align:center">🔥 Available Pets 🔥</h2>

<div class="grid">

<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png">
<h3>Axolotl Fly Ride</h3>
<div class="price">$2</div>
<div class="stock">⏳ Limited stock</div>
<button class="btn" onclick="addToCart('Axolotl Fly Ride',2)">Add to Cart</button>
</div>

<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg">
<h3>Cerberus Fly Ride</h3>
<div class="price">$3</div>
<div class="stock">⏳ Limited stock</div>
<button class="btn" onclick="addToCart('Cerberus Fly Ride',3)">Add to Cart</button>
</div>

<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png">
<h3>Dango Penguins</h3>
<div class="price">$10</div>
<div class="stock">⏳ Limited stock</div>
<button class="btn" onclick="addToCart('Dango Penguins',10)">Add to Cart</button>
</div>

<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png">
<h3>Neon Sneak Weasel (5)</h3>
<div class="price">$12</div>
<div class="stock">⏳ Limited stock</div>
<button class="btn" onclick="addToCart('Neon Sneak Weasel (5)',12)">Add to Cart</button>
</div>

<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg">
<h3>Ride Sakura Spirit</h3>
<div class="price">$8</div>
<div class="stock">⏳ Limited stock</div>
<button class="btn" onclick="addToCart('Ride Sakura Spirit',8)">Add to Cart</button>
</div>

<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg">
<h3>Snow Owl Fly Ride</h3>
<div class="price">$2.50</div>
<div class="stock">⏳ Limited stock</div>
<button class="btn" onclick="addToCart('Snow Owl Fly Ride',2.5)">Add to Cart</button>
</div>

</div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout</button>
</div>

<script>
let cart=[];

function addToCart(name,price){
cart.push({name,price});
renderCart();
}

function renderCart(){
let items=document.getElementById("cart-items");
let total=0;
items.innerHTML="";
cart.forEach((i,idx)=>{
total+=i.price;
items.innerHTML+=`
<div class="cart-item">
<span>${i.name}</span>
<span>$${i.price}</span>
</div>`;
});
document.getElementById("total").innerText=total.toFixed(2);
}

function checkout(){
if(cart.length===0){
alert("Your cart is empty!");
return;
}
let text="Oceanzx Order:\\n";
let total=0;
cart.forEach(i=>{
text+=`- ${i.name} $${i.price}\\n`;
total+=i.price;
});
text+=`Total: $${total}`;
navigator.clipboard.writeText(text);
window.open("https://discord.com/users/1455058787257024512","_blank");
}

/* anti inspect (basic) */
document.addEventListener('contextmenu',e=>e.preventDefault());
document.addEventListener('keydown',e=>{
if(e.key==="F12"||(e.ctrlKey&&e.shiftKey&&["I","J","C"].includes(e.key))||(e.ctrlKey&&e.key==="U")){
e.preventDefault();
}
});

/* particles */
for(let i=0;i<80;i++){
let d=document.createElement("div");
d.className="dot";
d.style.left=Math.random()*100+"vw";
d.style.animationDuration=(8+Math.random()*18)+"s";
document.body.appendChild(d);
}
</script>

</body>
</html>
