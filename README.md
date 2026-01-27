<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OCEANZX • Adopt Me Shop</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:#000;
  color:#fff;
}
header{
  padding:30px;
  text-align:center;
  border-bottom:1px solid #222;
}
header h1{
  margin:0;
  letter-spacing:4px;
}
header p{color:#aaa}

.container{
  max-width:1200px;
  margin:30px auto;
  padding:20px;
}

.section-title{
  font-size:24px;
  margin:40px 0 20px;
  border-bottom:1px solid #222;
  padding-bottom:10px;
}

.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
  gap:25px;
}

.card{
  background:#0e0e0e;
  border:1px solid #1f1f1f;
  border-radius:14px;
  padding:18px;
  text-align:center;
  transition:.25s;
}
.card:hover{
  transform:translateY(-4px);
  border-color:#fff;
}
.card img{
  width:100%;
  height:180px;
  object-fit:contain;
  background:#000;
  border-radius:12px;
}
.card h3{
  margin:12px 0 4px;
  font-size:16px;
}
.price{
  font-weight:bold;
  margin-top:6px;
}
.deal{
  font-size:12px;
  color:#aaa;
}
.stock{
  font-size:12px;
  margin-top:6px;
  color:#ccc;
}
.btn{
  margin-top:10px;
  padding:10px;
  width:100%;
  background:#fff;
  color:#000;
  border:none;
  border-radius:10px;
  font-weight:bold;
  cursor:pointer;
}
.btn:hover{opacity:.85}
.btn:disabled{
  background:#444;
  color:#999;
  cursor:not-allowed;
}

/* CART */
#cart{
  position:fixed;
  top:20px;
  right:20px;
  width:320px;
  background:#0e0e0e;
  border:1px solid #222;
  border-radius:16px;
  padding:16px;
}
#cart h3{margin-top:0}
#cart-items{
  max-height:260px;
  overflow-y:auto;
}
.cart-item{
  display:flex;
  justify-content:space-between;
  font-size:14px;
  margin:6px 0;
}
.cart-total{
  margin-top:10px;
  font-weight:bold;
}
.checkout{
  margin-top:10px;
  background:#fff;
  color:#000;
}

/* scrollbar */
#cart-items::-webkit-scrollbar{width:6px}
#cart-items::-webkit-scrollbar-thumb{background:#444;border-radius:10px}
</style>
</head>

<body>

<header>
  <h1>OCEANZX</h1>
  <p>Adopt Me • Clean • Trusted • Cash App Only</p>
</header>

<div class="container">

  <div class="section-title">🥚 Eggs</div>
  <div class="grid" id="eggs-grid"></div>

  <div class="section-title">🔥 Pets</div>
  <div class="grid" id="pets-grid"></div>

</div>

<div id="cart">
  <h3>🛒 Cart</h3>
  <div id="cart-items"></div>
  <div class="cart-total">Total: $<span id="total">0.00</span></div>
  <button class="btn checkout" onclick="checkout()">Checkout</button>
</div>

<script>
// ================= DATA =================

// EGGS (STOCK 15)
const eggs = [
 {name:"Crystal Egg", price:1.00, stock:15, deal:"$1 each", img:"https://image2url.com/r2/default/images/1769419308180-be119059-935c-4323-8d8a-2d0e5958128c.png"},
 {name:"Retired Egg", price:0.50, stock:15, deal:"2 for $1", img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
 {name:"Moon Egg", price:0.63, stock:15, deal:"2 for $1.25", img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
 {name:"Royal Egg", price:0.20, stock:15, deal:"5 for $1", img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"},
 {name:"Aussie Egg", price:5.00, stock:15, deal:"2 for $10", img:"https://image2url.com/r2/default/images/1769419333612-f58ec7fc-55d9-40d9-805d-16492cc76ff6.png"}
];

// PETS (STOCK 5)
const pets = [
 {name:"Axolotl Fly Ride", price:2.00, stock:5, img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png"},
 {name:"Cerberus Fly Ride", price:3.00, stock:5, img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg"},
 {name:"Dango Penguins", price:10.00, stock:5, img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png"},
 {name:"Neon Sneak Weasel (5)", price:12.00, stock:5, img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png"},
 {name:"Ride Sakura Spirit", price:8.00, stock:5, img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg"},
 {name:"Snow Owl Fly Ride", price:2.50, stock:5, img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg"},

 {name:"Strawberry Shortcake Bat Dragon Fly Ride", price:24.00, stock:5, img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
 {name:"Cow Fly Ride", price:20.00, stock:5, img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
 {name:"Chocolate Chip Bat Dragon Fly Ride", price:20.00, stock:5, img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png"},
 {name:"Dragonfruit Fox", price:12.50, stock:5, img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png"},
 {name:"Unicorn", price:3.25, stock:5, img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"},
 {name:"German Shepherd Fly Ride", price:11.20, stock:5, img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png"},
 {name:"Turtle Fly Ride", price:22.10, stock:5, img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"}
];

let cart = [];

// ================= RENDER =================
function renderSection(list, el, isEgg){
  el.innerHTML="";
  list.forEach((i,idx)=>{
    const c=document.createElement("div");
    c.className="card";
    c.innerHTML=`
      <img src="${i.img}">
      <h3>${i.name}</h3>
      <div class="price">$${i.price.toFixed(2)}</div>
      ${isEgg?`<div class="deal">${i.deal}</div>`:""}
      <div class="stock">Stock: ${i.stock}</div>
      <button class="btn" ${i.stock<=0?"disabled":""}
      onclick="addToCart(${isEgg?'eggs':'pets'},${idx})">
      ${i.stock<=0?"Sold Out":"Add to Cart"}
      </button>`;
    el.appendChild(c);
  });
}

function addToCart(arr,idx){
  if(arr[idx].stock<=0) return;
  arr[idx].stock--;
  cart.push({name:arr[idx].name,price:arr[idx].price});
  render();
}

function renderCart(){
  const el=document.getElementById("cart-items");
  let total=0;
  el.innerHTML="";
  cart.forEach(i=>{
    total+=i.price;
    el.innerHTML+=`<div class="cart-item"><span>${i.name}</span><span>$${i.price.toFixed(2)}</span></div>`;
  });
  document.getElementById("total").innerText=total.toFixed(2);
}

function checkout(){
  if(!cart.length) return alert("Cart empty");
  let text="OCEANZX ORDER\n\n";
  let total=0;
  cart.forEach(i=>{text+=`• ${i.name} - $${i.price}\n`; total+=i.price});
  text+=`\nTotal: $${total.toFixed(2)}\nCashApp ONLY: $Bananaboy723`;
  navigator.clipboard.writeText(text);
  window.open("https://discord.gg/sv6tRJBR5G","_blank");
  cart=[];
  render();
}

function render(){
  renderSection(eggs,document.getElementById("eggs-grid"),true);
  renderSection(pets,document.getElementById("pets-grid"),false);
  renderCart();
}

render();
</script>

</body>
</html>
