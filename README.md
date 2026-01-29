<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Oceanzx Adopt Me Shop</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:#000;
  color:#fff;
  padding-right:340px;
}

/* WHITE DOTS BACKGROUND */
body::before{
  content:"";
  position:fixed;
  inset:0;
  background:
    radial-gradient(2px 2px at 20px 30px,#fff 40%,transparent 41%),
    radial-gradient(2px 2px at 120px 90px,#fff 40%,transparent 41%),
    radial-gradient(2px 2px at 220px 160px,#fff 40%,transparent 41%);
  background-size:200px 200px;
  animation:dotsMove 2.5s linear infinite;
  opacity:.35;
  pointer-events:none;
  z-index:-1;
}
@keyframes dotsMove{
  from{background-position:0 0}
  to{background-position:-200px -200px}
}

/* TOP BAR */
.top-bar{
  text-align:center;
  padding:12px;
  background:#111;
  border-bottom:1px solid #222;
  font-weight:bold;
}

/* HEADER */
header{
  text-align:center;
  padding:20px;
}
header p{opacity:.8}

/* SECTIONS */
.section{
  padding:20px;
}
.section h2{
  border-bottom:1px solid #222;
  padding-bottom:6px;
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
  gap:15px;
}
.card{
  background:#111;
  border:1px solid #222;
  padding:12px;
  text-align:center;
}
.card img{
  width:100%;
  height:140px;
  object-fit:contain;
}
.card button{
  width:100%;
  margin-top:8px;
  padding:8px;
  border:none;
  border-radius:14px;
  background:#fff;
  color:#000;
  font-weight:bold;
  cursor:pointer;
}

/* CART */
.cart{
  position:fixed;
  top:90px;
  right:20px;
  width:300px;
  max-height:75vh;
  background:#111;
  border-radius:18px;
  padding:16px;
  overflow-y:auto;
  box-shadow:0 0 25px rgba(255,255,255,.08);
}
.cart h3{margin-top:0}
.cart-item{
  border-bottom:1px solid #222;
  padding:8px 0;
  font-size:14px;
}
.checkout-btn{
  margin-top:12px;
  width:100%;
  padding:12px;
  border:none;
  border-radius:16px;
  background:#fff;
  color:#000;
  font-weight:bold;
  cursor:pointer;
}

/* RECEIPT */
#receiptBox{
  width:100%;
  margin-top:10px;
  height:140px;
  background:#000;
  color:#fff;
  border-radius:14px;
  padding:10px;
  font-size:12px;
  border:1px solid #222;
}

footer{
  text-align:center;
  padding:20px;
  border-top:1px solid #222;
}
footer a{color:#fff;text-decoration:none}
</style>
</head>

<body>

<div class="top-bar">
🔥 10x Royal Egg — $7 • $10 OFF $45 ORDERS • Ends FEB 1st
</div>

<header>
  <h1>Oceanzx Adopt Me Shop</h1>
  <p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="section">
<h2>⭐ Featured Deals</h2>
<div class="grid" id="featured"></div>
</div>

<div class="section">
<h2>🐾 Pets</h2>
<div class="grid" id="pets"></div>
</div>

<div class="section">
<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>
</div>

<!-- CART -->
<div class="cart">
<h3>🛒 Cart</h3>
<div id="cartItems"></div>
<p><strong>Total: $<span id="total">0</span></strong></p>

<button class="checkout-btn" onclick="checkoutDiscord()">Checkout via Discord</button>

<textarea id="receiptBox" readonly></textarea>

<button class="checkout-btn" onclick="copyReceipt()">Copy Receipt</button>
</div>

<footer>
<p>Discord Support: <a href="https://discord.gg/sv6tRJBR5G" target="_blank">Join Here</a></p>
</footer>

<script>
let cart=[], total=0;

function add(item){
  cart.push(item);
  total+=item.price;
  renderCart();
}
function renderCart(){
  const c=document.getElementById("cartItems");
  c.innerHTML="";
  cart.forEach(i=>{
    const d=document.createElement("div");
    d.className="cart-item";
    d.textContent=i.name+" — $"+i.price;
    c.appendChild(d);
  });
  document.getElementById("total").textContent=total.toFixed(2);
}

function checkoutDiscord(){
  generateReceipt();
  window.open("https://discord.gg/sv6tRJBR5G","_blank");
}

function generateReceipt(){
  let id=Math.floor(100000+Math.random()*900000);
  let text=`🧾 OCEANZX RECEIPT
━━━━━━━━━━━━━━━━
Order ID: #${id}

Items:
`;
  cart.forEach(i=>{
    text+=`• ${i.name} — $${i.price}\n`;
  });
  text+=`
━━━━━━━━━━━━━━━━
Total: $${total.toFixed(2)}

Payment: Discord
Server: https://discord.gg/sv6tRJBR5G
━━━━━━━━━━━━━━━━`;
  document.getElementById("receiptBox").value=text;
}

function copyReceipt(){
  const b=document.getElementById("receiptBox");
  b.select();
  document.execCommand("copy");
  alert("Receipt copied. Paste it in Discord.");
}

/* DATA */
const featured=[
 {name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
 {name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"}
];

const pets=[
 {name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
 {name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg"},
 {name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
 {name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"},
 {name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"},
 {name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png"},
 {name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png"},
 {name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png"},
 {name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769571888116-fe636100-1ac8-4c9c-aaeb-0bfd97d9adb1.jpg"},
 {name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769571952502-156e70c2-979b-4008-a84e-d3dbab31f72d.webp"},
 {name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769572019588-bb64eee7-b0d3-40cc-9fa6-8a09e3dc8a51.jpg"}
];

const eggs=[
 {name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png"},
 {name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
 {name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
 {name:"Royal Egg (10x)",price:7,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"}
];

function render(list,id){
  const g=document.getElementById(id);
  list.forEach(i=>{
    const c=document.createElement("div");
    c.className="card";
    c.innerHTML=`
      <img src="${i.img}">
      <p>${i.name}</p>
      <p>$${i.price}</p>
      <button>Add to Cart</button>`;
    c.querySelector("button").onclick=()=>add(i);
    g.appendChild(c);
  });
}

render(featured,"featured");
render(pets,"pets");
render(eggs,"eggs");
</script>

</body>
</html>
