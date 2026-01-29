<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
body{
  margin:0;
  font-family:Arial, sans-serif;
  background:#000;
  color:#fff;
  overflow-x:hidden;
}

/* FAST WHITE DOTS BACKGROUND */
.dot{
  position:fixed;
  width:3px;
  height:3px;
  background:white;
  border-radius:50%;
  opacity:0.7;
  animation:float linear infinite;
  z-index:0;
}
@keyframes float{
  from{transform:translateY(-10vh);}
  to{transform:translateY(110vh);}
}

/* TOP BAR */
.top-bar{
  background:#fff;
  color:#000;
  text-align:center;
  padding:10px;
  font-weight:bold;
  font-size:14px;
  position:sticky;
  top:0;
  z-index:10;
}

/* SECTION HEADINGS */
section{
  padding:20px;
  position:relative;
  z-index:1;
}

h2{
  margin-bottom:10px;
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
  gap:15px;
}

/* CARD */
.card{
  background:#111;
  border-radius:20px;
  padding:14px;
  text-align:center;
}

.card img{
  width:100%;
  height:120px;
  object-fit:contain;
  border-radius:18px;
}

.card button{
  margin-top:8px;
  padding:8px;
  width:100%;
  border:none;
  border-radius:12px;
  background:#fff;
  color:#000;
  font-weight:bold;
  cursor:pointer;
}

.card button:disabled{
  background:#444;
  color:#999;
  cursor:not-allowed;
}

/* CART */
.cart{
  background:#111;
  border-radius:20px;
  padding:15px;
  max-width:400px;
  margin:20px auto;
}

.cart-item{
  display:flex;
  justify-content:space-between;
  margin-bottom:6px;
}

.checkout{
  margin-top:10px;
  width:100%;
  padding:10px;
  border:none;
  border-radius:14px;
  background:#00ffcc;
  font-weight:bold;
  cursor:pointer;
}
</style>
</head>
<body>

<!-- FAST DOTS -->
<script>
for(let i=0;i<80;i++){
  let d=document.createElement("div");
  d.className="dot";
  d.style.left=Math.random()*100+"vw";
  d.style.animationDuration=(5+Math.random()*10)+"s";
  document.body.appendChild(d);
}
</script>

<!-- TOP BAR -->
<div class="top-bar">
  💸 $10 OFF $45 ORDERS — Ends FEB 1st
</div>

<!-- EGGS SECTION -->
<section>
<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>
</section>

<!-- PETS SECTION -->
<section>
<h2>🐾 Pets</h2>
<div class="grid" id="pets"></div>
</section>

<!-- CART -->
<section>
<h2>🛒 Cart</h2>
<div class="cart">
  <div id="cartItems"></div>
  <hr>
  Total: $<span id="total">0.00</span>
  <button class="checkout" onclick="checkout()">Checkout (Discord)</button>
</div>
</section>

<script>
// EGG DATA
let eggs=[
{name:"Crystal Egg",price:1,stock:15,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png"},
{name:"Retired Egg",price:2,stock:15,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
{name:"Moon Egg",price:1.25,stock:15,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
{name:"Royal Egg",price:5,stock:15,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"},
{name:"10x Royal Egg",price:5,stock:10,img:"https://i.imgur.com/5VQ6F0R.png"}
];

// PET DATA (old + new)
let pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,stock:4,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
{name:"Cow Fly Ride",price:20,stock:4,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,stock:3,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"},
{name:"Dragonfruit Fox",price:12.5,stock:4,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg"},
{name:"Unicorn",price:3.25,stock:5,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
{name:"German Shepherd Fly Ride",price:11.2,stock:5,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"},
{name:"Turtle Fly Ride",price:22.1,stock:5,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"},
{name:"Snow Owl NO POT",price:1.25,stock:4,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png"},
{name:"Reindeer Fly Ride",price:2.3,stock:5,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png"},
{name:"Axolotl Fly Ride",price:2,stock:5,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png"},
{name:"Cerberus Fly Ride",price:3,stock:5,img:"https://image2url.com/r2/default/images/1769571888116-fe636100-1ac8-4c9c-aaeb-0bfd97d9adb1.jpg"},
{name:"Ride Sakura Spirit",price:8,stock:5,img:"https://image2url.com/r2/default/images/1769571952502-156e70c2-979b-4008-a84e-d3dbab31f72d.webp"},
{name:"Neon Sneak Weasel (5)",price:12,stock:5,img:"https://image2url.com/r2/default/images/1769572019588-bb64eee7-b0d3-40cc-9fa6-8a09e3dc8a51.jpg"},
{name:"Sneak Weasel",price:12,stock:5,img:"https://image2url.com/r2/default/images/1769571416593-b6e07468-7b7b-459e-b558-68041278a9e5.jpg"},
{name:"Dango",price:10,stock:5,img:"https://image2url.com/r2/default/images/1769571447431-5827c598-c3bf-41c2-af58-3ab54ed28eb2.webp"}
];

// CART
let cart=[];

// RENDER FUNCTION
function render(list,id){
  const container=document.getElementById(id);
  container.innerHTML="";
  list.forEach((item,i)=>{
    container.innerHTML+=`
      <div class="card">
        <img src="${item.img}" />
        <h4>${item.name}</h4>
        <p>$${item.price}</p>
        <p id="${id}-stock-${i}">Stock: ${item.stock}</p>
        <button onclick="add('${id}',${i})" ${item.stock<=0?"disabled":""}>
          Add to Cart
        </button>
      </div>
    `;
  });
}

function add(type,i){
  const list=type==="pets"?pets:eggs;
  if(list[i].stock<=0)return;
  list[i].stock--;
  cart.push({name:list[i].name,price:list[i].price});
  document.getElementById(`${type}-stock-${i}`).textContent="Stock: "+list[i].stock;
  updateCart();
}

function updateCart(){
  let total=0;
  const box=document.getElementById("cartItems");
  box.innerHTML="";
  cart.forEach(item=>{
    total+=item.price;
    box.innerHTML+=`<div class="cart-item"><span>${item.name}</span><span>$${item.price}</span></div>`;
  });
  document.getElementById("total").textContent=total.toFixed(2);
}

function checkout(){
  if(cart.length===0) return alert("Cart empty");
  // open discord link
  window.open("https://discord.gg/YOURDISCORD","_blank");
}

// INIT
render(eggs,"eggs");
render(pets,"pets");
</script>
</body>
</html>
