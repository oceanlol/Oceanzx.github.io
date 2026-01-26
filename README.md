<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
:root {
  --bg:#000;
  --card:#111;
  --text:#fff;
  --accent:#fff;
  --highlight:#888;
}
body {
  margin:0; font-family:Arial; background:var(--bg); color:var(--text);
}
header {
  text-align:center; padding:20px; border-bottom:1px solid var(--highlight);
}
header h1 { font-size:2.5rem; margin:0; }
header p { margin:5px 0; color:var(--highlight); font-size:1rem; }

.container { max-width:1200px; margin:20px auto; padding:0 15px; }
h2 { font-size:1.8rem; margin:20px 0 10px; border-bottom:1px solid var(--highlight); padding-bottom:5px; }
.grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(180px,1fr)); gap:20px; }

.card {
  background: var(--card);
  border-radius:15px; padding:15px; text-align:center;
  transition: transform 0.3s, box-shadow 0.3s;
}
.card:hover { transform:translateY(-5px); box-shadow:0 0 15px var(--highlight); }
.card img { width:150px; height:150px; object-fit:cover; border-radius:12px; }
.card h3 { margin:10px 0 5px; font-size:1rem; }
.card .price { color: var(--highlight); font-weight:bold; margin-bottom:5px; }
.card button {
  padding:6px 12px; border-radius:10px; border:none;
  background:var(--text); color:var(--bg); cursor:pointer; font-weight:bold;
}
.card button:hover { transform:scale(1.05); }

#cart {
  position:fixed; top:20px; right:20px; width:320px;
  background:var(--card); border-radius:20px; padding:15px;
  box-shadow:0 0 20px var(--highlight);
}
#cart h3 { margin-top:0; text-align:center; }
.cart-item {
  display:flex; align-items:center; justify-content:space-between;
  margin:5px 0; font-size:0.9rem;
}
.cart-item img { width:40px; height:40px; border-radius:6px; margin-right:5px; }
.cart-total { margin-top:10px; font-weight:bold; text-align:right; }
.btn-checkout {
  width:100%; padding:8px; background:var(--text); color:var(--bg);
  border:none; border-radius:10px; font-weight:bold; cursor:pointer;
}
.btn-checkout:hover { transform:scale(1.05); }
</style>
</head>
<body>
<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Adopt Me • Clean • Trusted • 👀 <span id="viewers">0</span> people viewing</p>
</header>

<div class="container">
<h2>🥚 Eggs Section</h2>
<div class="grid" id="eggs-grid"></div>

<h2>🔥 Pets Section</h2>
<div class="grid" id="pets-grid"></div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn-checkout" onclick="checkout()">Checkout</button>
</div>

<audio id="add-sound" src="https://www.soundjay.com/buttons/sounds/button-16.mp3"></audio>

<script>
// ---------------------- DATA ----------------------
let viewers = Math.floor(Math.random()*20+10);
document.getElementById("viewers").innerText = viewers;

let cart = [];

const discountCode = "OCEANZ10";

const items = [
  // EGGS
  {name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274c23a.png",stock:5,rarity:"rare"},
  {name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769418420566-8274c23a.png",stock:5,rarity:"rare"},
  {name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769418420566-8274c23a.png",stock:5,rarity:"epic"},
  {name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769418455991-0cd50c08.png",stock:5,rarity:"legendary"},
  {name:"Aussie Egg",price:10,img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef.png",stock:5,rarity:"epic"},

  // OLD PETS
  {name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82.png",stock:2,rarity:"epic"},
  {name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92.png",stock:2,rarity:"legendary"},
  {name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d.png",stock:3,rarity:"rare"},
  {name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97.png",stock:2,rarity:"epic"},
  {name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769312623274-1c54447a.png",stock:1,rarity:"legendary"},
  {name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769312555909-e343e380.png",stock:2,rarity:"epic"},
  {name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1.png",stock:1,rarity:"legendary"},
  {name:"Snow Owl Fly Ride",price:2.5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6.png",stock:4,rarity:"rare"},

  // NEW PETS
  {name:"Strawberry Shortcake Bat Dragon Fly Ride",price:35,img:"https://image2url.com/r2/default/images/1769417417556-2117c23b.png",stock:2,rarity:"legendary"},
  {name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417494592-7c9b625a.png",stock:2,rarity:"epic"},
  {name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f.png",stock:2,rarity:"epic"},
  {name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769417684237-e455a114.png",stock:3,rarity:"epic"},
  {name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb.png",stock:3,rarity:"rare"},
  {name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79.png",stock:2,rarity:"epic"},
  {name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242.png",stock:2,rarity:"legendary"}
];

// ---------------------- RENDER ----------------------
function renderItems(){
  const eggsGrid = document.getElementById("eggs-grid");
  const petsGrid = document.getElementById("pets-grid");
  eggsGrid.innerHTML = ""; petsGrid.innerHTML = "";
  items.forEach(item=>{
    const card = document.createElement("div");
    card.className="card";
    card.innerHTML = `
      <img src="${item.img}" alt="${item.name}">
      <h3>${item.name}</h3>
      <div class="price">$${item.price}</div>
      <div class="stock">Stock: ${item.stock}</div>
      <button onclick="addToCart('${item.name}')">Add to Cart</button>
    `;
    if(item.name.toLowerCase().includes("egg")) eggsGrid.appendChild(card);
    else petsGrid.appendChild(card);
  });
}

function addToCart(name){
  const item = items.find(i=>i.name===name);
  if(!item || item.stock<=0) return;
  cart.push(item);
  item.stock--;
  document.getElementById("add-sound").play();
  renderItems();
  renderCart();
}

function renderCart(){
  const cartEl = document.getElementById("cart-items");
  let total=0;
  cartEl.innerHTML="";
  cart.forEach((i,idx)=>{
    total+=i.price;
    cartEl.innerHTML+=`<div class="cart-item">
      <span>${i.name}</span>
      <span>$${i.price}</span>
      <span style="cursor:pointer;color:red;" onclick="removeFromCart(${idx})">❌</span>
    </div>`;
  });
  document.getElementById("total").innerText = total.toFixed(2);
}

function removeFromCart(idx){
  const item = cart.splice(idx,1)[0];
  const original = items.find(i=>i.name===item.name);
  if(original) original.stock++;
  renderItems();
  renderCart();
}

function checkout(){
  if(cart.length===0) return alert("Cart is empty!");
  let id = Math.floor(Math.random()*900000+100000);
  let text=`🛒 Oceanzx Order (ID:${id})\n`;
  let total=0;
  cart.forEach(i=>{ text+=`• ${i.name} - $${i.price}\n`; total+=i.price });
  text+=`\n💰 Total: $${total.toFixed(2)}`;
  navigator.clipboard.writeText(text);
  alert("Order copied! Send it in Discord.");
  window.open("https://discord.gg/sv6tRJBR5G","_blank");
  cart=[]; renderCart(); renderItems();
}

// ---------------------- INIT ----------------------
renderItems();
renderCart();
</script>
</body>
</html>
