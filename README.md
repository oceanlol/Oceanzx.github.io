<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
:root{
  --accent:#ffffff;
  --bg:#000000;
  --card:#111111;
  --text:#ffffff;
}
*{box-sizing:border-box;}
body{margin:0;font-family:Segoe UI,Arial,sans-serif;background:var(--bg);color:var(--text);overflow-x:hidden;scroll-behavior:smooth;}

/* WHITE DOTS */
.dot{position:fixed;width:3px;height:3px;background:white;border-radius:50%;opacity:.8;animation:float linear infinite;}
@keyframes float{from{transform:translateY(-10vh)}to{transform:translateY(120vh);}}

/* HEADER */
header{text-align:center;padding:30px;}
header h1{margin:0;font-size:2.8rem;color:var(--accent);}
header p{color:#aaa;font-size:1.2rem;margin-top:8px;}

/* CONTAINER */
.container{max-width:1200px;margin:20px auto;padding:20px;}

/* SECTION HEADINGS */
.container h2{text-align:center;font-size:2rem;margin-bottom:16px;position:relative;}
.container h2::after{content:"";display:block;width:80px;height:3px;background:var(--accent);margin:8px auto;border-radius:2px;}

/* GRID */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:28px;}

/* CARD */
.card{background:var(--card);border-radius:20px;padding:18px;text-align:center;transition:.35s;position:relative;overflow:hidden;cursor:pointer;}
.card img{width:150px;height:150px;object-fit:contain;border-radius:20px;}
.card:hover{transform:translateY(-5px);box-shadow:0 0 20px #fff;}

/* PRICE & STOCK */
.price{color:#ccc;font-weight:bold;margin-top:6px;}
.stock{color:#ff4d4d;font-size:.9rem;margin-top:4px;}

/* BUTTON */
.btn{background:none;border:2px solid #fff;padding:10px 20px;border-radius:18px;color:#fff;font-weight:bold;cursor:pointer;margin-top:8px;transition:.3s;}
.btn:hover{background:#fff;color:#000;}

/* CART */
#cart{position:fixed;top:20px;right:20px;background:#111;border-radius:24px;padding:16px;width:300px;transition:0.3s;box-shadow:0 0 30px rgba(255,255,255,.2);z-index:999;max-height:80vh;overflow-y:auto;}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;font-size:.9rem;}
.cart-item span:first-child{color:red;cursor:pointer;}
.cart-total{margin-top:10px;font-weight:bold;}
</style>
</head>
<body>
<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Adopt Me • Clean • Trusted</p>
</header>

<div class="container">
<h2>🐾 Pets Section 🐾</h2>
<div class="grid" id="pets-grid"></div>

<h2>🥚 Eggs Section 🥚</h2>
<div class="grid" id="eggs-grid"></div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout via Discord</button>
</div>

<script>
// WHITE DOTS
for(let i=0;i<100;i++){
  let d=document.createElement("div");
  d.className="dot";
  d.style.left=Math.random()*100+"vw";
  d.style.animationDuration=(5+Math.random()*10)+"s";
  document.body.appendChild(d);
}

// PETS
let pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:5},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:5},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:5},
{name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg",stock:5},
{name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",stock:5},
{name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",stock:5},
{name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",stock:5},
{name:"Sneak Weasel",price:20,img:"https://image2url.com/r2/default/images/1769571416593-b6e07468-7b7b-459e-b558-68041278a9e5.jpg",stock:5},
{name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769571447431-5827c598-c3bf-41c2-af58-3ab54ed28eb2.webp",stock:5},
{name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769571888116-fe636100-1ac8-4c9c-aaeb-0bfd97d9adb1.jpg",stock:5},
{name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769571952502-156e70c2-979b-4008-a84e-d3dbab31f72d.webp",stock:5},
{name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769572019588-bb64eee7-b0d3-40cc-9fa6-8a09e3dc8a51.jpg",stock:5},
{name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:5},
{name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png",stock:5},
{name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:5}
];

// EGGS
let eggs=[
{name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png",stock:15},
{name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png",stock:15},
{name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png",stock:15},
{name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15}
];

let cart=JSON.parse(localStorage.getItem("oceanzx-cart"))||[];

function renderItems(){
  const petsGrid=document.getElementById("pets-grid");
  const eggsGrid=document.getElementById("eggs-grid");
  petsGrid.innerHTML=""; eggsGrid.innerHTML="";
  pets.forEach(p=>{
    const card=document.createElement("div"); card.className="card";
    card.innerHTML=`<img src="${p.img}"><h3>${p.name}</h3><div class="price">$${p.price}</div><div class="stock" data-stock="${p.name}">Stock: ${p.stock}</div><button class="btn" onclick="addToCart('${p.name}')">Add to Cart</button>`;
    petsGrid.appendChild(card);
  });
  eggs.forEach(e=>{
    const card=document.createElement("div"); card.className="card";
    card.innerHTML=`<img src="${e.img}"><h3>${e.name}</h3><div class="price">$${e.price}</div><div class="stock" data-stock="${e.name}">Stock: ${e.stock}</div><button class="btn" onclick="addToCart('${e.name}')">Add to Cart</button>`;
    eggsGrid.appendChild(card);
  });
}

function findItem(name){return pets.concat(eggs).find(i=>i.name===name);}
function addToCart(name){
  const it=findItem(name); if(!it||it.stock<=0)return;
  cart.push({name,price:it.price}); it.stock--; updateStock(name); renderCart();
}
function updateStock(name){const it=findItem(name); const s=document.querySelector(`[data-stock="${name}"]`); if(it.stock<=0){s.innerText="Sold Out";}else{s.innerText="Stock: "+it.stock;}}
function renderCart(){const itemsEl=document.getElementById("cart-items"); let total=0; itemsEl.innerHTML=""; cart.forEach((i,idx)=>{total+=i.price; itemsEl.innerHTML+=`<div class="cart-item"><span onclick="removeFromCart(${idx})">❌</span><span>${i.name}</span><span>$${i.price}</span></div>`;}); document.getElementById("total").innerText=total.toFixed(2); localStorage.setItem("oceanzx-cart",JSON.stringify(cart));}
function removeFromCart(idx){const r=cart.splice(idx,1)[0]; const it=findItem(r.name); if(it) it.stock++; updateStock(r.name); renderCart();}
function checkout(){if(cart.length===0)return alert("Cart empty"); let id=Math.floor(Math.random()*900000+100000); let text=`🛒 Oceanzx Order (ID:${id})\n`; let total=0; cart.forEach(i=>{text+=`• ${i.name} - $${i.price}\n`; total+=i.price}); text+=`\n💰 Total: $${total.toFixed(2)}`; navigator.clipboard.writeText(text); window.open("https://discord.com/users/1455058787257024512","_blank"); cart=[]; renderCart(); localStorage.removeItem("oceanzx-cart");}

renderItems();
renderCart();
</script>
</body>
</html>
