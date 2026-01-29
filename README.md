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
  --border:#222;
  --text:#fff;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:var(--bg);
  color:var(--text);
  padding-right:320px;
}

/* TOP DEAL BAR */
.top-deal{
  background:#111;
  border-bottom:1px solid #222;
  padding:10px;
  text-align:center;
  font-weight:bold;
}

/* HEADER */
header{
  padding:20px;
  text-align:center;
}
header h1{margin:0}
header p{opacity:.8}

/* SECTIONS */
.section{
  padding:20px;
}
.section h2{
  border-bottom:1px solid #222;
  padding-bottom:5px;
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
  gap:15px;
}
.card{
  background:var(--card);
  border:1px solid var(--border);
  padding:10px;
  text-align:center;
}
.card img{
  width:100%;
  height:140px;
  object-fit:contain;
}
.card button{
  margin-top:8px;
  padding:8px;
  width:100%;
  background:#fff;
  color:#000;
  border:none;
  cursor:pointer;
  font-weight:bold;
}

/* CART (SIDE) */
.cart{
  position:fixed;
  top:0;
  right:0;
  width:300px;
  height:100%;
  background:#0a0a0a;
  border-left:1px solid #222;
  padding:15px;
  overflow-y:auto;
}
.cart h3{margin-top:0}
.cart-item{
  border-bottom:1px solid #222;
  padding:8px 0;
  font-size:14px;
}

/* FOOTER */
footer{
  padding:20px;
  text-align:center;
  border-top:1px solid #222;
}
footer a{color:#fff;text-decoration:none}
</style>
</head>

<body>

<div class="top-deal">
🔥 10x Royal Egg — $7 • $10 OFF $45 ORDERS • Ends on FEB 1st
</div>

<header>
  <h1>Oceanzx Adopt Me Shop</h1>
  <p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="section">
<h2>⭐ Featured Deals</h2>
<div class="grid" id="featured"></div>
</div>

<div class="section">
<h2>🐾 Pets</h2>
<div class="grid" id="pets"></div>
</div>

<div class="section">
<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>
</div>

<!-- CART -->
<div class="cart">
<h3>🛒 Cart</h3>
<div id="cartItems"></div>
<p><strong>Total: $<span id="total">0</span></strong></p>
</div>

<footer>
<p>Discord Support: <a href="https://discord.gg/sv6tRJBR5G" target="_blank">Join Here</a></p>
</footer>

<script>
let cart=[];
let total=0;

function add(item){
  cart.push(item);
  total+=item.price;
  renderCart();
}

function renderCart(){
  const c=document.getElementById("cartItems");
  c.innerHTML="";
  cart.forEach(i=>{
    const d=document.createElement("div");
    d.className="cart-item";
    d.textContent=i.name+" - $"+i.price;
    c.appendChild(d);
  });
  document.getElementById("total").textContent=total.toFixed(2);
}

const featuredPets=[
 {name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
 {name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"}
];

const pets=[
 {name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
 {name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg"},
 {name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
 {name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"}
];

const eggs=[
 {name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png"},
 {name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
 {name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
 {name:"Royal Egg (10x Bundle)",price:7,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"}
];

function render(list,id){
  const g=document.getElementById(id);
  list.forEach(i=>{
    const c=document.createElement("div");
    c.className="card";
    c.innerHTML=`
      <img src="${i.img}">
      <p>${i.name}</p>
      <p>$${i.price}</p>
      <button>Add to Cart</button>
    `;
    c.querySelector("button").onclick=()=>add(i);
    g.appendChild(c);
  });
}

render(featuredPets,"featured");
render(pets,"pets");
render(eggs,"eggs");
</script>

</body>
</html>
