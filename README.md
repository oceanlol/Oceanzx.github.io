<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=1200">
<title>OCEANZX – Adopt Me Shop</title>

<style>
:root{
  --bg:#0a0a0a;
  --card:#141414;
  --border:#2a2a2a;
  --text:#ffffff;
  --muted:#9a9a9a;
  --accent:#ffffff;
}
*{box-sizing:border-box}
body{
  margin:0;
  background:var(--bg);
  color:var(--text);
  font-family:Inter,Segoe UI,Arial,sans-serif;
}
header{
  padding:40px 20px;
  text-align:center;
  border-bottom:1px solid var(--border);
}
header h1{
  margin:0;
  font-size:48px;
  letter-spacing:3px;
}
header p{
  margin-top:8px;
  color:var(--muted);
}
.viewers{
  margin-top:10px;
  font-size:14px;
  color:#ccc;
}
.container{
  max-width:1300px;
  margin:40px auto;
  padding:0 30px;
}
h2{
  margin:40px 0 20px;
  font-size:26px;
  border-left:4px solid white;
  padding-left:12px;
}
.grid{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:22px;
}
.card{
  background:var(--card);
  border:1px solid var(--border);
  border-radius:18px;
  padding:18px;
  text-align:center;
  transition:.25s;
}
.card:hover{
  transform:translateY(-6px);
  border-color:white;
}
.card img{
  width:100%;
  height:160px;
  object-fit:contain;
  margin-bottom:12px;
}
.card h3{
  margin:6px 0;
  font-size:16px;
}
.price{
  font-weight:bold;
  margin:4px 0;
}
.stock{
  font-size:12px;
  color:#aaa;
}
button{
  margin-top:10px;
  width:100%;
  padding:10px;
  border-radius:12px;
  border:1px solid white;
  background:black;
  color:white;
  cursor:pointer;
}
button:hover{background:white;color:black}
button:disabled{opacity:.4;cursor:not-allowed}

/* CART */
#cart{
  position:fixed;
  right:20px;
  top:100px;
  width:340px;
  background:#0f0f0f;
  border:1px solid var(--border);
  border-radius:22px;
  padding:16px;
}
#cart h3{text-align:center;margin:0 0 10px}
#cart-items{
  max-height:260px;
  overflow-y:auto;
}
.cart-item{
  display:flex;
  align-items:center;
  gap:10px;
  margin-bottom:8px;
  font-size:13px;
}
.cart-item img{
  width:38px;
  height:38px;
  object-fit:contain;
}
.cart-item span.remove{
  cursor:pointer;
  color:red;
}
.total{
  margin-top:10px;
  font-weight:bold;
  text-align:center;
}
.checkout{
  margin-top:12px;
  padding:12px;
  width:100%;
  border-radius:14px;
  background:white;
  color:black;
  border:none;
  font-weight:bold;
  cursor:pointer;
}

/* MODAL */
#checkoutModal{
  position:fixed;
  inset:0;
  background:rgba(0,0,0,.8);
  display:none;
  align-items:center;
  justify-content:center;
}
.modal{
  background:#0f0f0f;
  border:1px solid var(--border);
  border-radius:20px;
  padding:24px;
  width:420px;
}
.modal h4{text-align:center;margin-top:0}
.modal pre{
  background:black;
  padding:12px;
  border-radius:10px;
  font-size:12px;
  white-space:pre-wrap;
}
.modal button{
  margin-top:10px;
}
</style>
</head>

<body>

<header>
  <h1>OCEANZX</h1>
  <p>Adopt Me • Clean • Trusted • CashApp Only</p>
  <div class="viewers">👀 <span id="viewers"></span> people viewing</div>
</header>

<div class="container">

<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>

<h2>🐾 Pets</h2>
<div class="grid" id="pets"></div>

</div>

<div id="cart">
  <h3>🛒 Cart</h3>
  <div id="cart-items"></div>
  <div class="total">Total: $<span id="total">0.00</span></div>
  <button class="checkout" onclick="openCheckout()">Checkout</button>
</div>

<div id="checkoutModal">
  <div class="modal">
    <h4>CashApp Checkout</h4>
    <p>Send payment to <b>$Bananaboy723</b></p>
    <pre id="orderText"></pre>
    <button onclick="copyOrder()">Copy Payment Note</button>
    <button onclick="window.open('https://cash.app/$Bananaboy723')">Open CashApp</button>
    <button onclick="window.open('https://discord.gg/sv6tRJBR5G')">Go to Discord</button>
    <button onclick="closeCheckout()">Close</button>
  </div>
</div>

<script>
document.getElementById("viewers").innerText =
  Math.floor(Math.random()*40)+12;

let cart=[];
const eggs=[
 {name:"Crystal Egg",price:1,stock:15,img:"https://image2url.com/r2/default/images/1769419308180-be119059-935c-4323-8d8a-2d0e5958128c.png"},
 {name:"Retired Egg",price:.5,stock:15,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
 {name:"Moon Egg",price:.63,stock:15,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
 {name:"Royal Egg",price:.2,stock:15,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"}
];

const pets=[
 {name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,stock:5,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
 {name:"Cow Fly Ride",price:20,stock:5,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
 {name:"Chocolate Chip Bat Dragon Fly Ride",price:20,stock:5,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"},
 {name:"Dragonfruit Fox",price:12.5,stock:5,img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png"},
 {name:"Unicorn",price:3.25,stock:5,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
 {name:"German Shepherd Fly Ride",price:11.2,stock:5,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"},
 {name:"Turtle Fly Ride",price:22.1,stock:5,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"},
 {name:"Axolotl Fly Ride",price:8,stock:5,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png"},
 {name:"Snow Owl Fly Ride",price:2.5,stock:5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg"},
 {name:"Snow Owl NO POT",price:1.75,stock:5,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png"},
 {name:"Ride Sakura Spirit",price:8,stock:5,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg"}
];

function render(section,data){
 const el=document.getElementById(section);
 data.forEach(i=>{
  const d=document.createElement("div");
  d.className="card";
  d.innerHTML=`
    <img src="${i.img}">
    <h3>${i.name}</h3>
    <div class="price">$${i.price}</div>
    <div class="stock">Stock: ${i.stock}</div>
    <button onclick='add("${section}","${i.name}")'>Add to Cart</button>`;
  el.appendChild(d);
 });
}

function add(section,name){
 const list=section==="eggs"?eggs:pets;
 const i=list.find(x=>x.name===name);
 if(i.stock<=0)return;
 cart.push(i);
 i.stock--;
 update();
}

function update(){
 const c=document.getElementById("cart-items");
 c.innerHTML="";
 let t=0;
 cart.forEach((i,idx)=>{
  t+=i.price;
  c.innerHTML+=`
   <div class="cart-item">
    <img src="${i.img}">
    <div>${i.name}</div>
    <div>$${i.price}</div>
    <span class="remove" onclick="remove(${idx})">✖</span>
   </div>`;
 });
 document.getElementById("total").innerText=t.toFixed(2);
 document.querySelectorAll(".grid").forEach(g=>g.innerHTML="");
 render("eggs",eggs); render("pets",pets);
}

function remove(i){
 cart[i].stock++;
 cart.splice(i,1);
 update();
}

function openCheckout(){
 if(!cart.length)return;
 let txt="OCEANZX ORDER\n";
 let total=0;
 cart.forEach(i=>{txt+=`• ${i.name}\n`; total+=i.price});
 txt+=`\nTOTAL: $${total.toFixed(2)}`;
 document.getElementById("orderText").innerText=txt;
 document.getElementById("checkoutModal").style.display="flex";
}
function closeCheckout(){
 document.getElementById("checkoutModal").style.display="none";
}
function copyOrder(){
 navigator.clipboard.writeText(document.getElementById("orderText").innerText);
 alert("Copied!");
}

render("eggs",eggs);
render("pets",pets);
</script>

</body>
</html>
