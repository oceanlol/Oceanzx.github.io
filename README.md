<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
:root{
  --bg:#000;
  --card:#111;
  --text:#fff;
  --accent:#fff;
  --radius:18px;
}
*{box-sizing:border-box;font-family:Arial,Helvetica,sans-serif}
body{margin:0;background:var(--bg);color:var(--text);overflow-x:hidden;position:relative}

.topbar{
  background:#fff;color:#000;text-align:center;padding:10px;font-weight:bold;
}

header{
  padding:25px;
}
h1{margin:0;font-size:28px}
.subtitle{opacity:.8}

main{
  display:flex;gap:20px;padding:20px;
}

.products{flex:3}

.section-title{font-size:22px;margin:25px 0 10px}

.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
  gap:15px;
}

.card{
  background:var(--card);
  border-radius:var(--radius);
  padding:12px;
  text-align:center;
}

.card img{width:100%;border-radius:12px;}

.card button{
  margin-top:8px;width:100%;padding:8px;border-radius:12px;border:none;cursor:pointer;
}

.cart{
  flex:1;
  background:var(--card);
  border-radius:var(--radius);
  padding:15px;
  position:sticky;
  top:20px;
  height:fit-content;
}

.cart-item{font-size:14px;margin-bottom:6px;}
.cart-total{margin-top:10px;font-weight:bold;}
.warning{color:#ff5555;font-size:13px;display:none;}
.checkout{
  margin-top:12px;padding:10px;border-radius:14px;background:#fff;color:#000;cursor:pointer;width:100%;border:none;
}

footer{text-align:center;opacity:.6;padding:20px}

/* white dots background */
.dot{position:absolute;width:3px;height:3px;background:#fff;border-radius:50%;animation:move 3s linear infinite;}
@keyframes move{0%{transform:translateY(0)}100%{transform:translateY(800px)}}
</style>
</head>
<body>

<div class="topbar">💸 $10 OFF $45 ORDERS • Ends FEB 1st</div>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<div class="subtitle">Fast Delivery • Trusted Trades • Discord Checkout</div>
</header>

<main>

<div class="products">

<div class="section-title">🔥 Featured Deal</div>
<div class="grid" id="featuredDeals"></div>

<div class="section-title">🐾 Pets</div>
<div class="grid" id="pets"></div>

<div class="section-title">🥚 Eggs</div>
<div class="grid" id="eggs"></div>

</div>

<div class="cart">
<h3>🛒 Your Cart</h3>
<div id="cartItems"></div>
<div class="cart-total" id="cartTotal">$0</div>
<div class="warning" id="warning">⚠️ Orders over $100 require Discord confirmation</div>
<button class="checkout" onclick="checkout()">Proceed to Discord</button>
</div>

</main>

<footer>Oceanzx © 2026 • Not affiliated with Roblox or Adopt Me</footer>

<!-- white dots -->
<script>
for(let i=0;i<100;i++){
  const d=document.createElement('div');
  d.classList.add('dot');
  d.style.left=Math.random()*window.innerWidth+'px';
  d.style.top=Math.random()*window.innerHeight+'px';
  d.style.animationDuration=(Math.random()*2+2)+'s';
  document.body.appendChild(d);
}
</script>

<!-- Firebase -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-app.js";
import { getDatabase, ref, set, onValue } from "https://www.gstatic.com/firebasejs/12.8.0/firebase-database.js";

const firebaseConfig = {
  apiKey: "AIzaSyAzsiK98Mz_YKW0Z8rWNd9ePuHbVRiUsZ4",
  authDomain: "tiktok-live-be8d8.firebaseapp.com",
  databaseURL: "https://tiktok-live-be8d8-default-rtdb.firebaseio.com",
  projectId: "tiktok-live-be8d8",
  storageBucket: "tiktok-live-be8d8.appspot.com",
  messagingSenderId: "228797898847",
  appId: "1:228797898847:web:b6cdfdb440827f586afbea"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

const sessionId = localStorage.getItem("oceanzx_id") || crypto.randomUUID();
localStorage.setItem("oceanzx_id", sessionId);
const cartRef = ref(db,"carts/"+sessionId);

let cart=[];

window.addToCart=(name,price)=>{
  cart.push({name,price});
  set(cartRef,cart);
};

onValue(cartRef,snap=>{
  cart=snap.val()||[];
  renderCart();
});

function renderCart(){
  const el=document.getElementById("cartItems");
  el.innerHTML="";
  let total=0;
  cart.forEach(i=>{total+=i.price;el.innerHTML+=`<div class="cart-item">${i.name} - $${i.price}</div>`});
  document.getElementById("cartTotal").innerText="$"+total.toFixed(2);
  document.getElementById("warning").style.display=total>=100?"block":"none";
}

window.checkout=()=>{
  let text="Oceanzx Order Receipt\n\n";
  cart.forEach(i=>text+=`${i.name} - $${i.price}\n`);
  text+="\nTotal: $"+cart.reduce((a,b)=>a+b.price,0);
  navigator.clipboard.writeText(text);
  window.location.href="https://discord.gg/sv6tRJBR5G";
};

// Data arrays
const featuredDeals=[
["10x Royal Egg",7,"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"]
];

const pets=[
["Strawberry Shortcake Bat Dragon Fly Ride",24,"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"],
["Cow Fly Ride",20,"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"],
["Chocolate Chip Bat Dragon Fly Ride",20,"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"],
["Dragonfruit Fox",12.5,"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg"],
["Unicorn",3.25,"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"],
["German Shepherd Fly Ride",11.2,"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"],
["Turtle Fly Ride",22.1,"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"],
["Snow Owl NO POT",1.25,"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png"],
["Reindeer Fly Ride",2.3,"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png"],
["Axolotl Fly Ride",2,"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png"],
["Cerberus Fly Ride",3,"https://image2url.com/r2/default/images/1769571888116-fe636100-1ac8-4c9c-aaeb-0bfd97d9adb1.jpg"],
["Ride Sakura Spirit",8,"https://image2url.com/r2/default/images/1769571952502-156e70c2-979b-4008-a84e-d3dbab31f72d.webp"],
["Neon Sneak Weasel (5)",12,"https://image2url.com/r2/default/images/1769572019588-bb64eee7-b0d3-40cc-9fa6-8a09e3dc8a51.jpg"]
];

const eggs=[
["Crystal Egg",1,"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png"],
["Retired Egg",2,"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"],
["Moon Egg",1.25,"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"],
["Royal Egg",5,"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"]
];

const petsDiv=document.getElementById("pets");
const eggsDiv=document.getElementById("eggs");
const featuredDiv=document.getElementById("featuredDeals");

// Render arrays
featuredDeals.forEach(p=>{
  featuredDiv.innerHTML+=`
  <div class="card">
    <img src="${p[2]}">
    <div>${p[0]}</div>
    <div>$${p[1]}</div>
    <button onclick="addToCart('${p[0]}',${p[1]})">Add to Cart</button>
  </div>`;
});

pets.forEach(p=>{
  petsDiv.innerHTML+=`
  <div class="card">
    <img src="${p[2]}">
    <div>${p[0]}</div>
    <div>$${p[1]}</div>
    <button onclick="addToCart('${p[0]}',${p[1]})">Add to Cart</button>
  </div>`;
});

eggs.forEach(e=>{
  eggsDiv.innerHTML+=`
  <div class="card">
    <img src="${e[2]}">
    <div>${e[0]}</div>
    <div>$${e[1]}</div>
    <button onclick="addToCart('${e[0]}',${e[1]})">Add to Cart</button>
  </div>`;
});
</script>
</body>
</html>
