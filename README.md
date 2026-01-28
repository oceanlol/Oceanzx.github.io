
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>OCEANZX — Adopt Me Shop</title>

<style>
:root{
  --bg:#000;
  --card:#0d0d0d;
  --border:#1f1f1f;
  --text:#fff;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Inter,Arial,sans-serif;
  background:var(--bg);
  color:var(--text);
  overflow-x:hidden;
}

/* flying dots */
.dot{
  position:fixed;
  background:#fff;
  border-radius:50%;
  opacity:.8;
  animation:fly linear infinite;
}
@keyframes fly{
  from{transform:translateY(120vh)}
  to{transform:translateY(-20vh)}
}

/* header */
header{
  padding:30px;
  text-align:center;
  border-bottom:1px solid var(--border);
}
header h1{margin:0;font-size:36px;letter-spacing:3px}
header p{opacity:.7}

/* layout */
section{padding:40px;max-width:1200px;margin:auto}
h2{margin-bottom:20px;letter-spacing:2px}

/* grid */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
  gap:25px;
}

/* product card */
.card{
  background:var(--card);
  border:1px solid var(--border);
  border-radius:18px;
  padding:20px;
  text-align:center;
}
.card img{
  width:100%;
  height:180px;
  object-fit:contain;
  filter:grayscale(100%) contrast(1.3) brightness(1.1);
  mix-blend-mode:lighten;
}
.card h3{font-size:16px;margin:15px 0 5px}
.card p{margin:4px 0;opacity:.8}

button{
  margin-top:10px;
  width:100%;
  padding:12px;
  background:#111;
  border:1px solid #333;
  color:#fff;
  border-radius:12px;
  cursor:pointer;
}
button:hover{background:#222}

/* cart */
#cartBtn{
  position:fixed;
  top:20px;
  right:20px;
  background:#fff;
  color:#000;
  border-radius:999px;
  padding:12px 18px;
  font-weight:bold;
}
#cart{
  position:fixed;
  inset:0;
  background:#000;
  display:none;
  padding:40px;
}
#cart h2{text-align:center}
.cart-items{
  max-height:60vh;
  overflow:auto;
  margin:30px 0;
}
.cart-item{
  display:flex;
  align-items:center;
  gap:15px;
  border-bottom:1px solid #222;
  padding:10px 0;
}
.cart-item img{
  width:60px;
  height:60px;
  object-fit:contain;
  filter:grayscale(100%) contrast(1.3);
  mix-blend-mode:lighten;
}
.total{font-size:20px;text-align:center;margin:20px 0}

.checkout{
  text-align:center;
}
.checkout button{
  max-width:300px;
  margin:auto;
  background:#fff;
  color:#000;
}

/* screenshot overlay */
#checkoutScreen{
  display:none;
  position:fixed;
  inset:0;
  background:#000;
  padding:40px;
  text-align:center;
}
#checkoutScreen h2{margin-bottom:20px}
#orderBox{
  border:1px dashed #555;
  padding:20px;
  max-width:500px;
  margin:auto;
}
</style>
</head>

<body>

<header>
  <h1>OCEANZX</h1>
  <p>Adopt Me • Clean • Trusted</p>
</header>

<button id="cartBtn" onclick="openCart()">Cart (<span id="cartCount">0</span>)</button>

<section>
<h2>PETS</h2>
<div class="grid" id="pets"></div>
</section>

<section>
<h2>EGGS</h2>
<div class="grid" id="eggs"></div>
</section>

<!-- CART -->
<div id="cart">
  <h2>Your Cart</h2>
  <div class="cart-items" id="cartItems"></div>
  <div class="total" id="total"></div>
  <div class="checkout">
    <button onclick="checkout()">Checkout</button><br><br>
    <button onclick="closeCart()">Close</button>
  </div>
</div>

<!-- CHECKOUT SCREEN -->
<div id="checkoutScreen">
  <h2>Almost Done</h2>
  <p>📸 Screenshot this and send it in the buying ticket</p>
  <div id="orderBox"></div>
  <p style="margin-top:20px">💸 Pay with Cash App: <b>$Bananaboy723</b></p>
  <button onclick="window.location.href='https://discord.gg/sv6tRJBR5G'">Go to Discord</button>
</div>

<script>
/* dots */
for(let i=0;i<120;i++){
  const d=document.createElement("div");
  d.className="dot";
  const s=Math.random()*3+1;
  d.style.width=d.style.height=s+"px";
  d.style.left=Math.random()*100+"vw";
  d.style.animationDuration=10+Math.random()*20+"s";
  document.body.appendChild(d);
}

/* products */
const pets=[
 {n:"Strawberry Shortcake Bat Dragon Fly Ride",p:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
 {n:"Cow Fly Ride",p:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
 {n:"Chocolate Chip Bat Dragon Fly Ride",p:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"},
 {n:"Dragonfruit Fox",p:12.5,img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png"},
 {n:"Unicorn",p:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
 {n:"German Shepherd Fly Ride",p:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"},
 {n:"Turtle Fly Ride",p:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"}
];

const eggs=[
 {n:"Crystal Egg",p:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png"},
 {n:"Retired Egg",p:0.5,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
 {n:"Moon Egg",p:0.63,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
 {n:"Royal Egg",p:0.2,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"}
];

const cart=[];
function render(list,id){
 const el=document.getElementById(id);
 list.forEach(i=>{
  el.innerHTML+=`
  <div class="card">
    <img src="${i.img}">
    <h3>${i.n}</h3>
    <p>$${i.p}</p>
    <p>Stock: ${id==="pets"?5:15}</p>
    <button onclick='add(${JSON.stringify(i)})'>Add to Cart</button>
  </div>`;
 });
}
render(pets,"pets");
render(eggs,"eggs");

function add(i){
 cart.push(i);
 document.getElementById("cartCount").innerText=cart.length;
}

function openCart(){
 document.getElementById("cart").style.display="block";
 const c=document.getElementById("cartItems");
 c.innerHTML="";
 let t=0;
 cart.forEach(i=>{
  t+=i.p;
  c.innerHTML+=`
  <div class="cart-item">
    <img src="${i.img}">
    <div>${i.n}<br>$${i.p}</div>
  </div>`;
 });
 document.getElementById("total").innerText="Total: $"+t.toFixed(2);
}
function closeCart(){document.getElementById("cart").style.display="none"}

function checkout(){
 document.getElementById("cart").style.display="none";
 document.getElementById("checkoutScreen").style.display="block";
 let text="<b>Your Order</b><br>";
 let t=0;
 cart.forEach(i=>{text+=i.n+" - $"+i.p+"<br>";t+=i.p});
 text+="<br><b>Total: $"+t.toFixed(2)+"</b>";
 document.getElementById("orderBox").innerHTML=text;
}
</script>
</body>
</html>
