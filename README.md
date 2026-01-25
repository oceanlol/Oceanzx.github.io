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
body{margin:0;font-family:Segoe UI,Arial,sans-serif;background:var(--bg);color:var(--text);overflow-x:hidden;}

/* particles */
.dot{position:fixed;width:3px;height:3px;background:white;border-radius:50%;opacity:.5;animation:float linear infinite;}
@keyframes float{from{transform:translateY(-10vh)}to{transform:translateY(120vh)}}

/* header */
header{text-align:center;padding:40px 20px;background:linear-gradient(180deg,#111,#000);border-bottom:1px solid #222;}
header h1{margin:0;font-size:2.3rem}
header p{color:#aaa}

/* trust bar */
.trust{background:#0a84ff;text-align:center;padding:10px;font-weight:bold;}

/* container */
.container{max-width:1200px;margin:30px auto;padding:25px;background:#121212;border-radius:30px;box-shadow:0 0 50px rgba(10,132,255,.15);}

/* grid */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:28px;}

/* card */
.card{background:linear-gradient(180deg,var(--card),#121212);border-radius:28px;padding:18px;text-align:center;transition:.35s;position:relative;}
.card:hover{transform:translateY(-6px);box-shadow:0 0 30px rgba(10,132,255,.4);}
.card img{width:150px;height:150px;object-fit:cover;border-radius:22px;}
.price{color:#ccc;font-weight:bold}
.stock{color:#ff4d4d;font-size:.8rem;animation:pulse 1.3s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.5}}

/* only 1 left flashing */
.only-one{animation:flash 0.8s infinite;}
@keyframes flash{0%,100%{opacity:1}50%{opacity:0.3}}

/* button */
.btn{background:linear-gradient(180deg,var(--accent),#0066cc);border:none;padding:10px 20px;border-radius:18px;color:white;font-weight:bold;cursor:pointer;margin-top:8px;}
.btn:hover{transform:scale(1.05)}

/* cart */
#cart{position:fixed;top:20px;right:20px;background:#121212;border-radius:24px;padding:16px;width:280px;box-shadow:0 0 30px rgba(0,0,0,.8);}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;font-size:.9rem;}
.cart-item span{cursor:pointer;}
.cart-total{margin-top:10px;font-weight:bold}

/* mobile */
@media(max-width:600px){#cart{width:240px}}

/* fake buyer popup */
.popup {position: fixed;bottom: 20px;left: -320px;background: #121212;border-radius: 16px;padding: 12px 16px;width: 260px;box-shadow: 0 0 25px rgba(0,0,0,.6);font-size: .85rem;z-index: 9999;animation: slideIn 0.6s forwards;}
.popup strong {color: #0a84ff;}
@keyframes slideIn {to { left: 20px; }}
@keyframes slideOut {to { left: -320px; opacity: 0; }}
</style>
</head>
<body>

<!-- KEY PROMPT -->
<div id="keyPrompt" style="position:fixed;top:0;left:0;width:100%;height:100%;background:#0b0b0b;display:flex;align-items:center;justify-content:center;flex-direction:column;z-index:9999;">
<h2 style="color:white;margin-bottom:10px;">Enter Key to Access</h2>
<input type="password" id="accessKey" placeholder="Enter Key" style="padding:10px;border-radius:8px;border:none;margin-bottom:10px;">
<button class="btn" onclick="checkKey()">Submit</button>
<p style="color:#aaa;margin-top:5px;">Hint: It's simple 😎</p>
</div>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="trust">✔ Instant Delivery • ✔ Trusted Trades • ✔ Discord Support</div>

<div class="container">

<h2 style="text-align:center">🔥 Available Pets 🔥</h2>
<div class="grid">

<!-- Axolotl Fly Ride -->
<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png">
<h3>Axolotl Fly Ride</h3>
<div class="price">$2</div>
<div class="stock" data-stock="Axolotl Fly Ride">⏳ Stock left: 3</div>
<button class="btn" data-btn="Axolotl Fly Ride" onclick="addToCart('Axolotl Fly Ride',2)">Add to Cart</button>
</div>

<!-- Cerberus Fly Ride -->
<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg">
<h3>Cerberus Fly Ride</h3>
<div class="price">$3</div>
<div class="stock" data-stock="Cerberus Fly Ride">⏳ Stock left: 2</div>
<button class="btn" data-btn="Cerberus Fly Ride" onclick="addToCart('Cerberus Fly Ride',3)">Add to Cart</button>
</div>

<!-- Dango Penguins -->
<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png">
<h3>Dango Penguins</h3>
<div class="price">$10</div>
<div class="stock" data-stock="Dango Penguins">⏳ Stock left: 1</div>
<button class="btn" data-btn="Dango Penguins" onclick="addToCart('Dango Penguins',10)">Add to Cart</button>
</div>

<!-- Neon Sneak Weasel -->
<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png">
<h3>Neon Sneak Weasel (5)</h3>
<div class="price">$12</div>
<div class="stock" data-stock="Neon Sneak Weasel (5)">⏳ Stock left: 2</div>
<button class="btn" data-btn="Neon Sneak Weasel (5)" onclick="addToCart('Neon Sneak Weasel (5)',12)">Add to Cart</button>
</div>

<!-- Ride Sakura Spirit -->
<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg">
<h3>Ride Sakura Spirit</h3>
<div class="price">$8</div>
<div class="stock" data-stock="Ride Sakura Spirit">⏳ Stock left: 1</div>
<button class="btn" data-btn="Ride Sakura Spirit" onclick="addToCart('Ride Sakura Spirit',8)">Add to Cart</button>
</div>

<!-- Snow Owl Fly Ride -->
<div class="card">
<img loading="lazy" src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg">
<h3>Snow Owl Fly Ride</h3>
<div class="price">$2.50</div>
<div class="stock" data-stock="Snow Owl Fly Ride">⏳ Stock left: 4</div>
<button class="btn" data-btn="Snow Owl Fly Ride" onclick="addToCart('Snow Owl Fly Ride',2.5)">Add to Cart</button>
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
// ===== KEY CHECK =====
function checkKey(){
  const key = document.getElementById("accessKey").value;
  if(key === "Keebs"){
    document.getElementById("keyPrompt").style.display="none";
  } else {
    alert("Incorrect Key 😤");
  }
}

// ===== CART & STOCK =====
let cart = [];

// Load cart from localStorage
const savedCart = JSON.parse(localStorage.getItem("oceanzx-cart"));
if(savedCart) cart = savedCart;

// stock
let stock = {
  "Axolotl Fly Ride": 3,
  "Cerberus Fly Ride": 2,
  "Dango Penguins": 1,
  "Neon Sneak Weasel (5)": 2,
  "Ride Sakura Spirit": 1,
  "Snow Owl Fly Ride": 4
};

// hold timers
let holdTimers = {};

// Add to cart
function addToCart(name, price){
  if(stock[name] <= 0) return;

  cart.push({name, price});
  stock[name]--;
  renderCart();
  updateStock(name);

  if(stock[name]===1){
    document.querySelector(`[data-stock="${name}"]`).classList.add("only-one");
  }

  if(holdTimers[name]) clearTimeout(holdTimers[name]);
  holdTimers[name] = setTimeout(()=>{
    stock[name]++;
    updateStock(name);
    renderCart();
  },300000);
}

// Update stock display
function updateStock(name){
  const stockEl = document.querySelector(`[data-stock="${name}"]`);
  const btn = document.querySelector(`[data-btn="${name}"]`);

  if(stock[name]<=0){
    stockEl.innerText="❌ SOLD OUT";
    btn.disabled=true;
    btn.innerText="Sold Out";
    btn.style.background="#444";
    stockEl.classList.remove("only-one");
  } else {
    stockEl.innerText=`⏳ Stock left: ${stock[name]}`;
    if(stock[name]>1) stockEl.classList.remove("only-one");
  }
}

// Render cart
function renderCart(){
  const items = document.getElementById("cart-items");
  let total = 0;
  items.innerHTML = "";

  cart.forEach((i,idx)=>{
    total+=i.price;
    items.innerHTML += `<div class="cart-item">
      <span onclick="removeFromCart(${idx})">❌</span>
      <span>${i.name}</span>
      <span>$${i.price}</span>
    </div>`;
  });

  document.getElementById("total").innerText = total.toFixed(2);
  // save to localStorage
  localStorage.setItem("oceanzx-cart", JSON.stringify(cart));
}

// Remove from cart
function removeFromCart(idx){
  const removed = cart.splice(idx,1)[0];
  stock[removed.name]++;
  clearTimeout(holdTimers[removed.name]);
  updateStock(removed.name);
  renderCart();
}

// Checkout
function checkout(){
  if(cart.length===0){alert("Cart empty!"); return;}
  const orderID = Math.floor(Math.random()*900000+100000);
  let order = `🛒 Oceanzx Order (ID:${orderID}):\n`;
  let total=0;
  cart.forEach(i=>{
    order+=`• ${i.name} - $${i.price}\n`;
    total+=i.price;
  });
  order+=`\n💰 Total: $${total.toFixed(2)}`;
  navigator.clipboard.writeText(order);
  window.open("https://discord.com/users/1455058787257024512","_blank");
  cart=[];
  renderCart();
  localStorage.removeItem("oceanzx-cart");
}

// ===== FAKE BUYERS =====
const fakeBuyers = ["xShadowWolf","LunaPlays","AdoptQueen","NeonTrader","RobloxKid88","MegaPets","StarrySky","FrostyX"];
const fakeItems = ["Axolotl Fly Ride","Cerberus Fly Ride","Snow Owl Fly Ride","Ride Sakura Spirit","Neon Sneak Weasel","Dango Penguins"];

function showFakePopup(){
  const buyer = fakeBuyers[Math.floor(Math.random()*fakeBuyers.length)];
  const item = fakeItems[Math.floor(Math.random()*fakeItems.length)];
  const popup = document.createElement("div");
  popup.className="popup";
  popup.innerHTML=`<strong>${buyer}</strong><br>bought <b>${item}</b><br><span style="color:#aaa">Just now</span>`;
  document.body.appendChild(popup);
  setTimeout(()=>{popup.style.animation="slideOut 0.6s forwards"; setTimeout(()=>popup.remove(),600);},5000);
}

setInterval(()=>{showFakePopup();}, Math.random()*12000+8000);

// ===== ANTI INSPECT =====
document.addEventListener('contextmenu',e=>e.preventDefault());
document.addEventListener('keydown',e=>{
if(e.key==="F12"||(e.ctrlKey&&e.shiftKey&&["I","J","C"].includes(e.key))||(e.ctrlKey&&e.key==="U")) e.preventDefault();
});

// ===== PARTICLES =====
for(let i=0;i<80;i++){
  const d=document.createElement("div");
  d.className="dot";
  d.style.left=Math.random()*100+"vw";
  d.style.animationDuration=(8+Math.random()*18)+"s";
  document.body.appendChild(d);
}
</script>
</body>
</html>
