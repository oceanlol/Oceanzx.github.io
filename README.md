<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OCEANZX</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{box-sizing:border-box;font-family:Arial,sans-serif}
body{
  margin:0;
  background:#000;
  color:#fff;
  overflow-x:hidden;
}

/* white dots */
body::before{
  content:"";
  position:fixed;
  inset:0;
  background:
    radial-gradient(2px 2px at 30px 40px,#fff 40%,transparent 41%),
    radial-gradient(2px 2px at 140px 120px,#fff 40%,transparent 41%),
    radial-gradient(2px 2px at 260px 200px,#fff 40%,transparent 41%);
  background-size:220px 220px;
  animation:dotsMove 2s linear infinite;
  opacity:.35;
  pointer-events:none;
  z-index:-1;
}
@keyframes dotsMove{
  from{background-position:0 0}
  to{background-position:-220px -220px}
}

/* top banner */
.banner{
  background:#fff;
  color:#000;
  text-align:center;
  padding:10px;
  font-weight:bold;
}

/* header */
header{
  padding:20px;
  text-align:center;
  font-size:32px;
  font-weight:bold;
}

/* layout */
.container{
  padding:20px;
  margin-right:340px;
}

/* sections */
.section-title{
  font-size:22px;
  margin:30px 0 15px;
}

/* grid */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
  gap:15px;
}

/* card */
.card{
  background:#111;
  border-radius:18px;
  padding:12px;
  text-align:center;
}
.card img{
  width:100%;
  height:140px;
  object-fit:contain;
  border-radius:14px;
}
.card button{
  margin-top:8px;
  width:100%;
  padding:8px;
  border:none;
  border-radius:14px;
  background:#fff;
  color:#000;
  font-weight:bold;
  cursor:pointer;
}

/* cart */
.cart{
  position:fixed;
  top:80px;
  right:20px;
  width:300px;
  max-height:75vh;
  background:#111;
  border-radius:18px;
  padding:16px;
  overflow-y:auto;
  box-shadow:0 0 25px rgba(255,255,255,.08);
}
.cart h3{text-align:center;margin-top:0}

.checkout-btn{
  width:100%;
  padding:12px;
  margin-top:10px;
  border:none;
  border-radius:16px;
  background:#fff;
  color:#000;
  font-weight:bold;
  cursor:pointer;
}
</style>
</head>

<body>

<div class="banner">$10 OFF $45 ORDERS • Ends on FEB 1st</div>
<header>OCEANZX</header>

<div class="cart">
  <h3>🛒 Cart</h3>
  <div id="cartItems"></div>
  <p id="cartTotal"></p>

  <button class="checkout-btn" onclick="checkoutDiscord()">Checkout via Discord</button>

  <textarea id="receiptBox" readonly style="
    width:100%;
    margin-top:10px;
    height:140px;
    background:#000;
    color:#fff;
    border-radius:14px;
    padding:10px;
    border:1px solid #222;
    font-size:12px;
  "></textarea>
</div>

<div class="container">

  <div class="section-title">🐾 Pets</div>
  <div class="grid" id="pets"></div>

  <div class="section-title">🥚 Eggs</div>
  <div class="grid" id="eggs"></div>

</div>

<script>
let cart=[], total=0;

let pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:4},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:4},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:3},
{name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769572512431-ffc2599d-7cf1-4d6e-aa1f-e975783dc761.jpg",stock:4},
{name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",stock:5},
{name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",stock:5},
{name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",stock:5},
{name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:4},
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
{name:"Royal Egg (10x)",price:7,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15}
];

function render(list,id){
  const el=document.getElementById(id);
  list.forEach(i=>{
    el.innerHTML+=`
    <div class="card">
      <img src="${i.img}">
      <div>${i.name}</div>
      <div>$${i.price}</div>
      <div>Stock: ${i.stock}</div>
      <button onclick="add('${i.name}',${i.price})">Add to Cart</button>
    </div>`;
  });
}

function add(name,price){
  cart.push({name,price});
  total+=price;
  updateCart();
}

function updateCart(){
  let out="";
  cart.forEach(i=>out+=`<div>${i.name} — $${i.price}</div>`);
  document.getElementById("cartItems").innerHTML=out;
  document.getElementById("cartTotal").innerText="Total: $"+total.toFixed(2);
}

function generateReceipt(){
  let id=Math.floor(100000+Math.random()*900000);
  let txt=`🧾 OCEANZX RECEIPT\n━━━━━━━━━━━━━━━━\nOrder ID: #${id}\n\nItems:\n`;
  cart.forEach(i=>txt+=`• ${i.name} — $${i.price}\n`);
  txt+=`\n━━━━━━━━━━━━━━━━\nTotal: $${total.toFixed(2)}\nServer: https://discord.gg/sv6tRJBR5G\n`;
  receiptBox.value=txt;
}

function checkoutDiscord(){
  generateReceipt();
  if(total>=100 && !confirm("⚠️ Large Order ($"+total.toFixed(2)+")\nConfirm before continuing."))return;
  receiptBox.select();
  document.execCommand("copy");
  window.open("https://discord.gg/sv6tRJBR5G","_blank");
}

render(pets,"pets");
render(eggs,"eggs");
</script>

</body>
</html>
