<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Oceanzx Adopt Me Shop</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root{
  --bg:#000;
  --card:#111;
  --text:#fff;
}

*{box-sizing:border-box}

body{
  margin:0;
  font-family:Segoe UI,Arial,sans-serif;
  background:var(--bg);
  color:var(--text);
  overflow-x:hidden;
  padding-top:55px;
}

/* PROMO BAR */
#promo-bar{
  position:fixed;
  top:0;left:0;
  width:100%;
  background:#000;
  color:#fff;
  text-align:center;
  padding:12px;
  font-weight:700;
  letter-spacing:1px;
  z-index:10000;
  box-shadow:0 0 20px rgba(255,255,255,.6);
  animation:promoGlow 2s infinite alternate;
}
@keyframes promoGlow{
  from{box-shadow:0 0 8px rgba(255,255,255,.3)}
  to{box-shadow:0 0 22px rgba(255,255,255,.9)}
}

/* WHITE DOTS */
.dot{
  position:fixed;
  width:3px;height:3px;
  background:white;
  border-radius:50%;
  opacity:.8;
  animation:float linear infinite;
}
@keyframes float{
  from{transform:translateY(-10vh)}
  to{transform:translateY(120vh)}
}

/* HEADER */
header{text-align:center;padding:30px}
header h1{font-size:2.6rem;margin:0}
header p{color:#aaa}

/* LAYOUT */
.container{max-width:1200px;margin:auto;padding:20px}
h2{text-align:center;margin:40px 0 20px}
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:25px;
}

/* CARD */
.card{
  background:var(--card);
  border-radius:24px;
  padding:18px;
  text-align:center;
  transition:.3s;
}
.card:hover{transform:translateY(-5px);box-shadow:0 0 25px #fff}
.card img{
  width:150px;
  height:150px;
  object-fit:contain;
  border-radius:24px;
}
.price{font-weight:bold;margin-top:6px}
.stock{color:#ff4d4d;font-size:.9rem}

/* BUTTON */
.btn{
  margin-top:10px;
  background:none;
  border:2px solid #fff;
  color:#fff;
  padding:10px 18px;
  border-radius:20px;
  cursor:pointer;
  transition:.3s;
}
.btn:hover{background:#fff;color:#000}

/* CART */
#cart{
  position:fixed;
  right:20px;
  top:90px;
  width:300px;
  max-height:75vh;
  overflow-y:auto;
  background:#111;
  border-radius:26px;
  padding:16px;
  box-shadow:0 0 30px rgba(255,255,255,.25);
  z-index:999;
}
.cart-item{
  display:flex;
  justify-content:space-between;
  font-size:.9rem;
  margin:6px 0;
}
.cart-item span:first-child{color:red;cursor:pointer}
.cart-total{margin-top:10px;font-weight:bold}
</style>
</head>

<body>

<div id="promo-bar">
🔥 $10 OFF $45 ORDERS • ENDS FEB 1ST 🔥
</div>

<header>
  <h1>Oceanzx Adopt Me Shop</h1>
  <p>Clean • Trusted • Fast Delivery</p>
</header>

<div class="container">

<h2>🐾 Pets</h2>
<div class="grid" id="pets"></div>

<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>

</div>

<div id="cart">
  <h3>🛒 Cart</h3>
  <div id="cart-items"></div>
  <div class="cart-total">Total: $<span id="total">0.00</span></div>
  <button class="btn" onclick="checkout()">Checkout via Discord</button>
</div>

<script>
// DOTS
for(let i=0;i<120;i++){
  let d=document.createElement("div");
  d.className="dot";
  d.style.left=Math.random()*100+"vw";
  d.style.animationDuration=(4+Math.random()*8)+"s";
  document.body.appendChild(d);
}

// DATA
let pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:5},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:5},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:5},
{name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg",stock:5},
{name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",stock:5},
{name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",stock:5},
{name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",stock:5},
{name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:5},
{name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png",stock:5},
{name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:5},
{name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769571888116-fe636100-1ac8-4c9c-aaeb-0bfd97d9adb1.jpg",stock:5},
{name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769571952502-156e70c2-979b-4008-a84e-d3dbab31f72d.webp",stock:5},
{name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769572019588-bb64eee7-b0d3-40cc-9fa6-8a09e3dc8a51.jpg",stock:5}
];

let eggs=[
{name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png",stock:15},
{name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png",stock:15},
{name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png",stock:15},
{name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15}
];

let cart=[];

function render(section,data){
  const el=document.getElementById(section);
  el.innerHTML="";
  data.forEach(i=>{
    const c=document.createElement("div");
    c.className="card";
    c.innerHTML=`
      <img src="${i.img}">
      <h3>${i.name}</h3>
      <div class="price">$${i.price}</div>
      <div class="stock">Stock: ${i.stock}</div>
      <button class="btn" onclick="add('${section}',${data.indexOf(i)})">Add to Cart</button>`;
    el.appendChild(c);
  });
}

function add(type,i){
  let item=(type==="pets"?pets:eggs)[i];
  if(item.stock<=0)return;
  cart.push(item);
  item.stock--;
  render("pets",pets);
  render("eggs",eggs);
  drawCart();
}

function drawCart(){
  let el=document.getElementById("cart-items");
  let total=0;
  el.innerHTML="";
  cart.forEach((i,idx)=>{
    total+=i.price;
    el.innerHTML+=`<div class="cart-item"><span onclick="cart.splice(${idx},1);drawCart()">❌</span><span>${i.name}</span><span>$${i.price}</span></div>`;
  });
  document.getElementById("total").innerText=total.toFixed(2);
}

function checkout(){
  if(!cart.length)return;
  let id=Math.floor(Math.random()*900000+100000);
  let text=`🛒 Oceanzx Order (ID:${id})\n`;
  let total=0;
  cart.forEach(i=>{text+=`• ${i.name} - $${i.price}\n`;total+=i.price});
  text+=`\nTotal: $${total.toFixed(2)}`;
  navigator.clipboard.writeText(text);
  window.open("https://discord.com/users/1455058787257024512","_blank");
  cart=[];
  drawCart();
}

render("pets",pets);
render("eggs",eggs);
</script>

</body>
</html>
