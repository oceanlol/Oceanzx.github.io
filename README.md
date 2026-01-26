<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
:root {
  --bg: #0b0b0b;
  --card: #1c1c1c;
  --text: #ffffff;
  --accent: #ffffff;
  --accent-hover: #ddd;
}
body {
  margin:0;
  font-family: Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
  overflow-x: hidden;
}

/* HEADER */
header {
  text-align: center;
  padding: 40px 20px;
  border-bottom: 2px solid #333;
}
header h1 {
  margin:0;
  font-size: 3rem;
  color: var(--accent);
}
header p {
  margin: 5px 0 0;
  font-size: 1.2rem;
  color:#aaa;
}

/* SECTION TITLES */
h2 {
  text-align: center;
  margin-top: 40px;
  font-size: 2rem;
  border-bottom: 1px solid #333;
  padding-bottom: 10px;
}

/* GRID */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(180px,1fr));
  gap: 20px;
  max-width: 1200px;
  margin: 20px auto;
}

/* CARD */
.card {
  background: var(--card);
  border-radius: 20px;
  padding: 15px;
  text-align: center;
  transition: transform 0.3s, box-shadow 0.3s;
}
.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 0 20px #555;
}
.card img {
  width: 150px;
  height: 150px;
  object-fit: cover;
  border-radius: 15px;
  margin-bottom: 8px;
}
.card h3 {
  font-size: 1rem;
  margin: 5px 0;
}
.card .price {
  font-weight: bold;
  margin-top: 5px;
}

/* BUTTON */
.btn {
  background: var(--accent);
  color: var(--bg);
  border: none;
  padding: 8px 12px;
  border-radius: 12px;
  cursor: pointer;
  margin-top: 8px;
  font-weight: bold;
  transition: all 0.2s;
}
.btn:hover {
  background: var(--accent-hover);
}

/* CART */
#cart {
  position: fixed;
  top: 20px;
  right: 20px;
  background: var(--card);
  width: 320px;
  max-height: 80vh;
  overflow-y: auto;
  border-radius: 20px;
  padding: 15px;
  box-shadow: 0 0 20px #000;
  z-index: 999;
}
#cart h3 { text-align:center; margin:0 0 10px; }
.cart-item {
  display:flex;
  align-items:center;
  justify-content: space-between;
  margin-bottom: 8px;
  font-size: 0.9rem;
}
.cart-item img {
  width: 40px;
  height: 40px;
  object-fit: cover;
  border-radius: 6px;
  margin-right: 6px;
}
.cart-total {
  font-weight: bold;
  margin-top: 10px;
  text-align: right;
}
.cart-item span.remove {
  cursor: pointer;
  color: red;
}

/* CHECKOUT */
.checkout-msg {
  text-align:center;
  font-size:0.9rem;
  margin-top:8px;
  color:#aaa;
}
</style>
</head>
<body>
<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Adopt Me • Clean • Trusted • 👀 27 people viewing</p>
</header>

<h2>🥚 Eggs</h2>
<div class="grid" id="eggs-grid"></div>

<h2>🔥 Pets</h2>
<div class="grid" id="pets-grid"></div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout</button>
<div class="checkout-msg">After checkout, take a screenshot of your cart and send it in the Discord ticket.</div>
</div>

<script>
// CART
let cart = [];

// EGGS DATA
const eggs = [
{name:"Crystal Egg", price:1, img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png", stock:5},
{name:"Retired Egg", price:2, img:"https://image2url.com/r2/default/images/1769418455991-0cd50c08-7af1-433f-8438-1ff08827d293.png", stock:5},
{name:"Moon Egg", price:1.25, img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png", stock:5},
{name:"Royal Egg", price:5, img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png", stock:5},
{name:"Aussie Egg", price:10, img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png", stock:5},
];

// PETS DATA (OLD + NEW)
const pets = [
{name:"Axolotl Fly Ride", price:2, img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png", stock:3},
{name:"Cerberus Fly Ride", price:3, img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg", stock:2},
{name:"Dango Penguins", price:10, img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png", stock:1},
{name:"Neon Sneak Weasel (5)", price:12, img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png", stock:2},
{name:"Ride Sakura Spirit", price:8, img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg", stock:1},
{name:"Snow Owl Fly Ride", price:2.5, img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg", stock:4},
{name:"Snow Owl NO POT", price:1.25, img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png", stock:2},
{name:"Reindeer Fly Ride", price:2.3, img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png", stock:2},

{name:"Strawberry Shortcake Bat Dragon Fly Ride", price:35, img:"https://image2url.com/r2/default/images/1769419308180-be119059-935c-4323-8d8a-2d0e5958128c.png", stock:2},
{name:"Cow Fly Ride", price:20, img:"https://image2url.com/r2/default/images/1769419333612-f58ec7fc-55d9-40d9-805d-16492cc76ff6.png", stock:20},
{name:"Chocolate Chip Bat Dragon Fly Ride", price:20, img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png", stock:20},
{name:"Dragonfruit Fox", price:12.5, img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png", stock:10},
{name:"Unicorn", price:3.25, img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png", stock:3},
{name:"German Shepherd Fly Ride", price:11.2, img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png", stock:5},
{name:"Turtle Fly Ride", price:22.1, img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png", stock:8},
];

// RENDER ITEMS
function renderGrid(gridId, data){
  const grid=document.getElementById(gridId);
  grid.innerHTML="";
  data.forEach(item=>{
    const card=document.createElement("div");
    card.className="card";
    card.innerHTML=`
      <img src="${item.img}" alt="${item.name}">
      <h3>${item.name}</h3>
      <div class="price">$${item.price}</div>
      <button class="btn" onclick="addToCart('${item.name}',${item.price})">Add to Cart</button>
    `;
    grid.appendChild(card);
  });
}

// ADD TO CART
function addToCart(name, price){
  const item = [...eggs,...pets].find(i=>i.name===name);
  if(!item || item.stock<=0) return;
  cart.push({name,price,img:item.img});
  item.stock--;
  updateCart();
}

// UPDATE CART
function updateCart(){
  const itemsEl=document.getElementById("cart-items");
  itemsEl.innerHTML="";
  let total=0;
  cart.forEach((i,idx)=>{
    total+=i.price;
    const div=document.createElement("div");
    div.className="cart-item";
    div.innerHTML=`
      <span class="remove" onclick="removeFromCart(${idx})">❌</span>
      <img src="${i.img}" alt="${i.name}">
      <span>${i.name}</span>
      <span>$${i.price}</span>
    `;
    itemsEl.appendChild(div);
  });
  document.getElementById("total").innerText=total.toFixed(2);
}

// REMOVE FROM CART
function removeFromCart(idx){
  const removed=cart.splice(idx,1)[0];
  const item=[...eggs,...pets].find(i=>i.name===removed.name);
  if(item) item.stock++;
  updateCart();
}

// CHECKOUT
function checkout(){
  if(cart.length===0) return alert("Cart is empty!");
  let total=0;
  let text="🛒 Oceanzx Order\n";
  cart.forEach(i=>{
    total+=i.price;
    text+=`• ${i.name} - $${i.price}\n`;
  });
  text+=`\n💰 Total: $${total.toFixed(2)}`;
  navigator.clipboard.writeText(text);
  alert("Cart copied! Now send in Discord ticket: https://discord.gg/sv6tRJBR5G");
  cart=[];
  updateCart();
}

// INITIAL RENDER
renderGrid("eggs-grid", eggs);
renderGrid("pets-grid", pets);
updateCart();
</script>
</body>
</html>
