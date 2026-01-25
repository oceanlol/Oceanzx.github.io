<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
:root{
--accent:#0a84ff;
--bg:#0b0b0b;
--card:#1c1c1c;
--text:#ffffff;
}
*{box-sizing:border-box}
body{margin:0;font-family:Segoe UI,Arial,sans-serif;background:var(--bg);color:var(--text);overflow-x:hidden}

/* particles */
.dot{position:fixed;width:3px;height:3px;background:white;border-radius:50%;opacity:.5;animation:float linear infinite}
@keyframes float{from{transform:translateY(-10vh)}to{transform:translateY(120vh)}}

/* header */
header{text-align:center;padding:40px 20px;background:linear-gradient(180deg,#111,#000)}
header h1{margin:0;font-size:2.3rem}
header p{color:#aaa}

/* trust bar */
.trust{background:#0a84ff;text-align:center;padding:10px;font-weight:bold}

/* container */
.container{max-width:1200px;margin:30px auto;padding:25px;background:#121212;border-radius:30px}

/* grid */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:28px}

/* card */
.card{background:linear-gradient(180deg,var(--card),#121212);border-radius:28px;padding:18px;text-align:center;transition:.35s;position:relative;}
.card:hover{transform:translateY(-6px)}
.card img{width:150px;height:150px;object-fit:cover;border-radius:22px}
.price{color:#ccc;font-weight:bold}
.stock{color:#ff4d4d;font-size:.8rem;animation:pulse 1.3s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.5}}
.only-one{animation:flash .8s infinite}
@keyframes flash{0%,100%{opacity:1}50%{opacity:.3}}

/* button */
.btn{background:linear-gradient(180deg,var(--accent),#0066cc);border:none;padding:10px 20px;border-radius:18px;color:white;font-weight:bold;cursor:pointer;margin-top:8px}

/* cart */
#cart{position:fixed;top:20px;right:20px;background:#121212;border-radius:24px;padding:16px;width:280px;transition:0.3s;}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;font-size:.9rem}
.cart-item span{cursor:pointer}
.cart-total{margin-top:10px;font-weight:bold}

/* mobile cart slide-in */
#cart.mobile-hide{right:-320px}
#cart.mobile-show{right:20px}
#cart-toggle{display:none;position:fixed;bottom:20px;right:20px;background:var(--accent);color:#fff;padding:10px 14px;border-radius:50%;font-weight:bold;cursor:pointer;z-index:9999}

/* fake popup */
.popup{position:fixed;bottom:20px;left:-320px;background:#121212;border-radius:16px;padding:12px 16px;width:260px;font-size:.85rem;animation:slideIn .6s forwards;z-index:9999;}
.popup strong{color:#0a84ff;}
@keyframes slideIn{to{left:20px}}
@keyframes slideOut{to{left:-320px;opacity:0}}

/* recently viewed notice */
.view-notice{position:absolute;top:8px;left:8px;background:#0a84ff;padding:4px 6px;border-radius:8px;font-size:.75rem;color:#fff;opacity:0;transition:opacity 0.3s;}
</style>
</head>
<body>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="trust">✔ Instant Delivery • ✔ Trusted Trades • ✔ Discord Support</div>

<div class="container">
<h2 style="text-align:center">🥚 Available Eggs 🥚</h2>
<div class="grid">

<!-- Crystal Egg -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769340250503-3d3f2972-9914-4529-9abd-abaf9b370d22.png">
<h3>Crystal Egg</h3>
<div class="price">$1</div>
<div class="stock" data-stock="Crystal Egg">⏳ Stock left: 3</div>
<div class="timer" data-timer="Crystal Egg"></div>
<button class="btn" data-btn="Crystal Egg" onclick="addToCart('Crystal Egg',1)">Add to Cart</button>
</div>

<!-- Snow Owl NO POT -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png">
<h3>Snow Owl NO POT</h3>
<div class="price">$1.25</div>
<div class="stock" data-stock="Snow Owl NO POT">⏳ Stock left: 2</div>
<div class="timer" data-timer="Snow Owl NO POT"></div>
<button class="btn" data-btn="Snow Owl NO POT" onclick="addToCart('Snow Owl NO POT',1.25)">Add to Cart</button>
</div>

<!-- Reindeer Fly Ride -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png">
<h3>Reindeer Fly Ride</h3>
<div class="price">$2.30</div>
<div class="stock" data-stock="Reindeer Fly Ride">⏳ Stock left: 2</div>
<div class="timer" data-timer="Reindeer Fly Ride"></div>
<button class="btn" data-btn="Reindeer Fly Ride" onclick="addToCart('Reindeer Fly Ride',2.3)">Add to Cart</button>
</div>

</div>

<h2 style="text-align:center">🔥 Available Pets 🔥</h2>
<div class="grid">

<!-- Axolotl Fly Ride -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png">
<h3>Axolotl Fly Ride</h3>
<div class="price">$2</div>
<div class="stock" data-stock="Axolotl Fly Ride">⏳ Stock left: 3</div>
<div class="timer" data-timer="Axolotl Fly Ride"></div>
<button class="btn" data-btn="Axolotl Fly Ride" onclick="addToCart('Axolotl Fly Ride',2)">Add to Cart</button>
</div>

<!-- Cerberus Fly Ride -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg">
<h3>Cerberus Fly Ride</h3>
<div class="price">$3</div>
<div class="stock" data-stock="Cerberus Fly Ride">⏳ Stock left: 2</div>
<div class="timer" data-timer="Cerberus Fly Ride"></div>
<button class="btn" data-btn="Cerberus Fly Ride" onclick="addToCart('Cerberus Fly Ride',3)">Add to Cart</button>
</div>

<!-- Dango Penguins -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png">
<h3>Dango Penguins</h3>
<div class="price">$10</div>
<div class="stock" data-stock="Dango Penguins">⏳ Stock left: 1</div>
<div class="timer" data-timer="Dango Penguins"></div>
<button class="btn" data-btn="Dango Penguins" onclick="addToCart('Dango Penguins',10)">Add to Cart</button>
</div>

<!-- Neon Sneak Weasel -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png">
<h3>Neon Sneak Weasel (5)</h3>
<div class="price">$12</div>
<div class="stock" data-stock="Neon Sneak Weasel (5)">⏳ Stock left: 2</div>
<div class="timer" data-timer="Neon Sneak Weasel (5)"></div>
<button class="btn" data-btn="Neon Sneak Weasel (5)" onclick="addToCart('Neon Sneak Weasel (5)',12)">Add to Cart</button>
</div>

<!-- Ride Sakura Spirit -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg">
<h3>Ride Sakura Spirit</h3>
<div class="price">$8</div>
<div class="stock" data-stock="Ride Sakura Spirit">⏳ Stock left: 1</div>
<div class="timer" data-timer="Ride Sakura Spirit"></div>
<button class="btn" data-btn="Ride Sakura Spirit" onclick="addToCart('Ride Sakura Spirit',8)">Add to Cart</button>
</div>

<!-- Snow Owl Fly Ride -->
<div class="card">
<div class="view-notice"></div>
<img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg">
<h3>Snow Owl Fly Ride</h3>
<div class="price">$2.50</div>
<div class="stock" data-stock="Snow Owl Fly Ride">⏳ Stock left: 4</div>
<div class="timer" data-timer="Snow Owl Fly Ride"></div>
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

<div id="cart-toggle">🛒</div>

<script>
// CART + STOCK + STORAGE
let cart = JSON.parse(localStorage.getItem("oceanzx-cart"))||[];
let stock={
"Crystal Egg":3,
"Snow Owl NO POT":2,
"Reindeer Fly Ride":2,
"Axolotl Fly Ride":3,
"Cerberus Fly Ride":2,
"Dango Penguins":1,
"Neon Sneak Weasel (5)":2,
"Ride Sakura Spirit":1,
"Snow Owl Fly Ride":4
};
let holdTimers={};
let restockTimers={};

// ADD TO CART
function addToCart(name,price){
if(stock[name]<=0)return;
cart.push({name,price});
stock[name]--;
updateStock(name);
renderCart();
showViewedNotice(name);

// HOLD 5 min
holdTimers[name]=setTimeout(()=>{
stock[name]++;
updateStock(name);
renderCart();
},300000);
}

// UPDATE STOCK + TIMER
function updateStock(name){
const s=document.querySelector(`[data-stock="${name}"]`);
const b=document.querySelector(`[data-btn="${name}"]`);
const timerEl=document.querySelector(`[data-timer="${name}"]`);

if(stock[name]<=0){
s.innerText="❌ SOLD OUT";
b.disabled=true;
b.innerText="Sold Out";

if(!restockTimers[name]){
let countdown=60; // restock 1 min
timerEl.innerText=`Restock in ${countdown}s`;
restockTimers[name]=setInterval(()=>{
countdown--;
timerEl.innerText=`Restock in ${countdown}s`;
if(countdown<=0){
clearInterval(restockTimers[name]);
delete restockTimers[name];
stock[name]=3; // reset stock default
updateStock(name);
timerEl.innerText="";
}
},1000);
}

}else{
s.innerText=`⏳ Stock left: ${stock[name]}`;
b.disabled=false;
b.innerText="Add to Cart";
timerEl.innerText="";
}
}

// RENDER CART
function renderCart(){
const items=document.getElementById("cart-items");
let total=0;
items.innerHTML="";
cart.forEach((i,idx)=>{
total+=i.price;
items.innerHTML+=`
<div class="cart-item">
<span onclick="removeFromCart(${idx})">❌</span>
<span>${i.name}</span>
<span>$${i.price}</span>
</div>`;
});
document.getElementById("total").innerText=total.toFixed(2);
localStorage.setItem("oceanzx-cart",JSON.stringify(cart));
}

// REMOVE FROM CART
function removeFromCart(idx){
const r=cart.splice(idx,1)[0];
stock[r.name]++;
updateStock(r.name);
renderCart();
}

// CHECKOUT
function checkout(){
if(cart.length===0)return alert("Cart empty");
const id=Math.floor(Math.random()*900000+100000);
let text=`🛒 Oceanzx Order (ID:${id})\n`;
let total=0;
cart.forEach(i=>{text+=`• ${i.name} - $${i.price}\n`;total+=i.price});
text+=`\n💰 Total: $${total.toFixed(2)}`;
navigator.clipboard.writeText(text);
window.open("https://discord.com/users/1455058787257024512","_blank");
cart=[];
localStorage.removeItem("oceanzx-cart");
renderCart();
}

// FAKE BUYERS
const names=["Jayden R.","Mia L.","Ethan P.","Noah T.","Ava S.","Lucas M.","Sophie K.","Ryan D.","Olivia B.","Daniel C."];
const itemsFake=["Axolotl Fly Ride","Cerberus Fly Ride","Snow Owl Fly Ride","Ride Sakura Spirit","Neon Sneak Weasel","Crystal Egg","Snow Owl NO POT","Reindeer Fly Ride"];
const sound=new Audio("https://assets.mixkit.co/sfx/preview/mixkit-message-pop-alert-2354.mp3");

function fakePopup(){
const p=document.createElement("div");
p.className="popup";
p.innerHTML=`<strong>${names[Math.floor(Math.random()*names.length)]}</strong><br>bought <b>${itemsFake[Math.floor(Math.random()*itemsFake.length)]}</b><br><span style="color:#aaa">Just now</span>`;
document.body.appendChild(p);
sound.volume=0.25; sound.play();
setTimeout(()=>{p.style.animation="slideOut .6s forwards"; setTimeout(()=>p.remove(),600)},5000);
}
setInterval(fakePopup,Math.random()*12000+8000);

// VIEWED NOTICE
function showViewedNotice(name){
const card=document.querySelector(`[data-stock="${name}"]`).closest(".card");
const notice=card.querySelector(".view-notice");
notice.innerText="👀 Someone viewed this!";
notice.style.opacity=1;
setTimeout(()=>{notice.style.opacity=0;},3000);
}

// ADMIN HOTKEY
document.addEventListener("keydown",e=>{
if(e.ctrlKey && e.shiftKey && e.key==="S"){
const p=prompt("Admin Password:");
if(p==="admin123"){
const item=prompt("Enter item name exactly:");
const qty=parseInt(prompt("Enter new stock quantity:"));
if(item && qty>=0){stock[item]=qty;updateStock(item);renderCart();alert("Stock updated")}}
}
});

// MOBILE CART TOGGLE
const cartToggle=document.getElementById("cart-toggle");
cartToggle.addEventListener("click",()=>{document.getElementById("cart").classList.toggle("mobile-show");});
window.addEventListener("resize",()=>{if(window.innerWidth>600){document.getElementById("cart").classList.remove("mobile-show");}});
if(window.innerWidth<=600)document.getElementById("cart").classList.add("mobile-hide");

// PARTICLES
for(let i=0;i<80;i++){let d=document.createElement("div");d.className="dot";d.style.left=Math.random()*100+"vw";d.style.animationDuration=(8+Math.random()*18)+"s";document.body.appendChild(d);}

// INITIAL RENDER
Object.keys(stock).forEach(updateStock);
renderCart();
</script>
</body>
</html>
