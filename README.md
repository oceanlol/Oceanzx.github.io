<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OCEANZX</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  margin:0;
  font-family:Segoe UI,Arial,sans-serif;
  background:#000;
  color:#fff;
  overflow-x:hidden;
}

/* PARTICLES */
.dot{
  position:fixed;
  width:3px;
  height:3px;
  background:white;
  opacity:.6;
  border-radius:50%;
  animation:fall linear infinite;
}
@keyframes fall{
  from{transform:translateY(-10vh)}
  to{transform:translateY(110vh)}
}

/* HEADER */
header{
  padding:40px 20px;
  text-align:center;
}
header h1{
  font-size:3rem;
  font-weight:900;
  letter-spacing:2px;
}
header p{opacity:.7}

/* CART (SIDE) */
#cart{
  position:fixed;
  top:0;
  right:0;
  width:320px;
  height:100vh;
  background:#000;
  border-left:2px solid #fff;
  padding:16px;
  z-index:999;
  display:flex;
  flex-direction:column;
}
#cart h3{
  margin:0;
  font-size:1.4rem;
  font-weight:900;
}
#cart-items{
  flex:1;
  overflow-y:auto;
  margin-top:12px;
}
.cart-item{
  display:flex;
  justify-content:space-between;
  font-size:.9rem;
  margin:8px 0;
}
.cart-total{
  font-weight:900;
  margin-top:10px;
}
.checkout{
  margin-top:10px;
  background:#fff;
  color:#000;
  border:2px solid #000;
  padding:10px;
  font-weight:900;
  cursor:pointer;
}

/* CONTENT */
.container{
  max-width:1200px;
  margin:40px auto;
  padding:20px;
  margin-right:360px;
}
h2{
  margin-top:50px;
  font-size:2rem;
  border-bottom:2px solid #fff;
  padding-bottom:6px;
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:25px;
  margin-top:20px;
}

/* CARD */
.card{
  background:#111;
  padding:18px;
  border-radius:18px;
  text-align:center;
  position:relative;
}
.card img{
  width:140px;
  height:140px;
  object-fit:contain;
}
.card h3{
  margin:10px 0 4px;
  font-weight:900;
}
.price{opacity:.9}
.stock{font-size:.8rem;opacity:.7}

/* BADGE */
.badge{
  position:absolute;
  top:10px;
  left:10px;
  background:#fff;
  color:#000;
  border:2px solid #000;
  font-size:12px;
  font-weight:900;
  padding:4px 8px;
}

/* BUTTON */
.btn{
  margin-top:10px;
  background:#fff;
  color:#000;
  border:2px solid #000;
  padding:8px 14px;
  font-weight:900;
  cursor:pointer;
}
.btn:disabled{
  opacity:.4;
  cursor:not-allowed;
}
</style>
</head>

<body>

<header>
  <h1>OCEANZX</h1>
  <p>Adopt Me • Clean • Trusted • CashApp Only</p>
</header>

<!-- CART -->
<div id="cart">
  <h3>🛒 Cart</h3>
  <div id="cart-items"></div>
  <div class="cart-total">Total: $<span id="total">0.00</span></div>
  <button class="checkout" onclick="checkout()">Checkout</button>
</div>

<div class="container">

<h2>🔥 New Pets</h2>
<div class="grid" id="newPets"></div>

<h2>🐾 Old Pets</h2>
<div class="grid" id="oldPets"></div>

<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>

</div>

<script>
let cart=[];

const items=[
  // NEW PETS
  {name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,stock:5,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",section:"new"},
  {name:"Cow Fly Ride",price:20,stock:5,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",section:"new"},

  // OLD PETS
  {name:"Chocolate Chip Bat Dragon Fly Ride",price:20,stock:5,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",section:"old"},
  {name:"Dragonfruit Fox",price:12.5,stock:5,img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png",section:"old"},
  {name:"Unicorn",price:3.25,stock:5,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",section:"old"},
  {name:"German Shepherd Fly Ride",price:11.2,stock:5,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",section:"old"},
  {name:"Turtle Fly Ride",price:22.1,stock:5,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",section:"old"},

  // EGGS
  {name:"Crystal Egg",price:1,stock:15,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png",section:"egg"},
  {name:"Retired Egg",price:0.5,stock:15,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png",section:"egg"},
  {name:"Moon Egg",price:0.63,stock:15,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png",section:"egg"},
  {name:"Royal Egg",price:0.2,stock:15,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",section:"egg"}
];

function render(){
  newPets.innerHTML="";
  oldPets.innerHTML="";
  eggs.innerHTML="";

  items.forEach(it=>{
    const card=document.createElement("div");
    card.className="card";
    card.innerHTML=`
      ${it.section==="new"?'<div class="badge">NEW</div>':""}
      <img src="${it.img}">
      <h3>${it.name}</h3>
      <div class="price">$${it.price}</div>
      <div class="stock">Stock: ${it.stock}</div>
      <button class="btn" ${it.stock<=0?"disabled":""} onclick="add('${it.name}')">Add to Cart</button>
    `;
    if(it.section==="new")newPets.appendChild(card);
    else if(it.section==="old")oldPets.appendChild(card);
    else eggs.appendChild(card);
  });
}

function add(name){
  const it=items.find(i=>i.name===name);
  if(!it||it.stock<=0)return;
  cart.push(it);
  it.stock--;
  updateCart();
  render();
}

function updateCart(){
  cartItems.innerHTML="";
  let total=0;
  cart.forEach(i=>{
    total+=i.price;
    cartItems.innerHTML+=`<div class="cart-item"><span>${i.name}</span><span>$${i.price}</span></div>`;
  });
  totalSpan.innerText=total.toFixed(2);
}

function checkout(){
  if(!cart.length)return;
  let text="OCEANZX ORDER:\n";
  let total=0;
  cart.forEach(i=>{text+=`• ${i.name} $${i.price}\n`;total+=i.price});
  text+=`\nTOTAL: $${total.toFixed(2)}\nCashApp: $Bananaboy723`;
  navigator.clipboard.writeText(text);
  alert("Order copied. Pay via CashApp.");
}

const cartItems=document.getElementById("cart-items");
const totalSpan=document.getElementById("total");

for(let i=0;i<120;i++){
  const d=document.createElement("div");
  d.className="dot";
  d.style.left=Math.random()*100+"vw";
  d.style.animationDuration=(6+Math.random()*14)+"s";
  document.body.appendChild(d);
}

render();
</script>
</body>
</html>
