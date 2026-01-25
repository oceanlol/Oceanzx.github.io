
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop - GOD MODE</title>
<style>
:root{
  --accent:#0a84ff;
  --rare:#8A2BE2;
  --epic:#FF69B4;
  --legendary:#FFD700;
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
.card{background:linear-gradient(180deg,var(--card),#121212);border-radius:28px;padding:18px;text-align:center;transition:.35s;position:relative;overflow:hidden;}
.card:hover{transform:translateY(-6px)}
.card img{width:150px;height:150px;object-fit:cover;border-radius:22px;transition:transform 0.3s;}
.card:hover img{transform:scale(1.08)}
.price{color:#ccc;font-weight:bold}
.stock{color:#ff4d4d;font-size:.8rem;animation:pulse 1.3s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.5}}
.only-one{animation:flash .8s infinite}
@keyframes flash{0%,100%{opacity:1}50%{opacity:.3}}

/* rarity outline */
.card.rare img{box-shadow:0 0 12px var(--rare);}
.card.epic img{box-shadow:0 0 12px var(--epic);}
.card.legendary img{box-shadow:0 0 12px var(--legendary);}

/* button */
.btn{background:linear-gradient(180deg,var(--accent),#0066cc);border:none;padding:10px 20px;border-radius:18px;color:white;font-weight:bold;cursor:pointer;margin-top:8px;transition:.3s}
.btn:hover{transform:scale(1.05)}

/* cart */
#cart{position:fixed;top:20px;right:20px;background:#121212;border-radius:24px;padding:16px;width:280px;transition:0.3s;}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;font-size:.9rem}
.cart-item span{cursor:pointer}
.cart-total{margin-top:10px;font-weight:bold}
#cart-toggle{display:none;position:fixed;bottom:20px;right:20px;background:var(--accent);color:#fff;padding:10px 14px;border-radius:50%;font-weight:bold;cursor:pointer;z-index:9999}

/* fake popup */
.popup{position:fixed;bottom:20px;left:-320px;background:#121212;border-radius:16px;padding:12px 16px;width:260px;font-size:.85rem;animation:slideIn .6s forwards;z-index:9999;}
.popup strong{color:var(--accent);}
@keyframes slideIn{to{left:20px}}
@keyframes slideOut{to{left:-320px;opacity:0}}

/* hatching animation */
.hatch{animation:hatchAnim 0.8s forwards}
@keyframes hatchAnim{0%{transform:scale(0);opacity:0}50%{transform:scale(1.2)}100%{transform:scale(1);opacity:1}}

/* viewed notice */
.view-notice{position:absolute;top:8px;left:8px;background:#0a84ff;padding:4px 6px;border-radius:8px;font-size:.75rem;color:#fff;opacity:0;transition:opacity 0.3s}
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
<div class="grid" id="eggs-grid"></div>

<h2 style="text-align:center">🔥 Available Pets 🔥</h2>
<div class="grid" id="pets-grid"></div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout</button>
</div>

<script>
// CART + STOCK
let cart = JSON.parse(localStorage.getItem("oceanzx-cart"))||[];
let items=[
  {name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769340250503-3d3f2972-9914-4529-9abd-abaf9b370d22.png",stock:3,rarity:"rare"},
  {name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:2,rarity:"epic"},
  {name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png",stock:2,rarity:"legendary"},
  {name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:3,rarity:"rare"},
  {name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg",stock:2,rarity:"epic"},
  {name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png",stock:1,rarity:"legendary"},
  {name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png",stock:2,rarity:"epic"},
  {name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg",stock:1,rarity:"legendary"},
  {name:"Snow Owl Fly Ride",price:2.5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg",stock:4,rarity:"rare"}
];

// RENDER ITEMS
function renderItems(){
  const eggsGrid=document.getElementById("eggs-grid");
  const petsGrid=document.getElementById("pets-grid");
  eggsGrid.innerHTML=""; petsGrid.innerHTML="";
  items.forEach(it=>{
    const card=document.createElement("div");
    card.className="card "+it.rarity;
    card.innerHTML=`
      <div class="view-notice"></div>
      <img src="${it.img}">
      <h3>${it.name}</h3>
      <div class="price">$${it.price}</div>
      <div class="stock" data-stock="${it.name}">⏳ Stock left: ${it.stock}</div>
      <button class="btn" data-btn="${it.name}" onclick="addToCart('${it.name}',${it.price})">Add to Cart</button>
    `;
    if(it.name.toLowerCase().includes("egg")){
      eggsGrid.appendChild(card);
    }else{
      petsGrid.appendChild(card);
    }
  });
}

// FIND ITEM
function findItem(name){return items.find(i=>i.name===name);}

// ADD TO CART
function addToCart(name,price){
  const it=findItem(name);
  if(!it||it.stock<=0)return;
  cart.push({name,price});
  it.stock--;
  updateStock(name);
  renderCart();
  showViewedNotice(name);
  // HATCH animation if egg
  if(name.toLowerCase().includes("egg")){
    const imgEl=document.querySelector(`[data-stock="${name}"]`).closest(".card").querySelector("img");
    imgEl.classList.add("hatch");
    setTimeout(()=>{imgEl.classList.remove("hatch")},800);
  }
  // hold 5 min
  setTimeout(()=>{
    it.stock++;
    updateStock(name);
    renderCart();
  },300000);
}

// UPDATE STOCK
function updateStock(name){
  const it=findItem(name);
  const s=document.querySelector(`[data-stock="${name}"]`);
  const b=document.querySelector(`[data-btn="${name}"]`);
  if(it.stock<=0){
    s.innerText="❌ SOLD OUT";
    b.disabled=true;
    b.innerText="Sold Out";
    if(it.stock===0) s.classList.add("only-one");
  }else{
    s.innerText=`⏳ Stock left: ${it.stock}`;
    b.disabled=false;
    b.innerText="Add to Cart";
    s.classList.remove("only-one");
  }
}

// RENDER CART
function renderCart(){
  const itemsEl=document.getElementById("cart-items");
  let total=0;
  itemsEl.innerHTML="";
  cart.forEach((i,idx)=>{
    total+=i.price;
    itemsEl.innerHTML+=`
      <div class="cart-item">
        <span onclick="removeFromCart(${idx})">❌</span>
        <span>${i.name}</span>
        <span>$${i.price}</span>
      </div>`;
  });
  document.getElementById("total").innerText=total.toFixed(2);
  localStorage.setItem("oceanzx-cart",JSON.stringify(cart));
}

// REMOVE ITEM
function removeFromCart(idx){
  const r=cart.splice(idx,1)[0];
  const it=findItem(r.name);
  if(it) it.stock++;
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
  cart=[]; localStorage.removeItem("oceanzx-cart"); renderCart();
}

// FAKE BUYERS
const names=["Jayden R.","Mia L.","Ethan P.","Noah T.","Ava S.","Lucas M.","Sophie K.","Ryan D.","Olivia B.","Daniel C."];
const itemsFake=items.map(i=>i.name);

function fakePopup(){
  const p=document.createElement("div");
  p.className="popup";
  p.innerHTML=`<strong>${names[Math.floor(Math.random()*names.length)]}</strong> bought <b>${itemsFake[Math.floor(Math.random()*itemsFake.length)]}</b><br><span style="color:#aaa">Just now</span>`;
  document.body.appendChild(p);
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

// PARTICLES
for(let i=0;i<80;i++){let d=document.createElement("div");d.className="dot";d.style.left=Math.random()*100+"vw";d.style.animationDuration=(8+Math.random()*18)+"s";document.body.appendChild(d);}

// INITIAL RENDER
renderItems();
items.forEach(it=>updateStock(it.name));
renderCart();
</script>
</body>
</html>
