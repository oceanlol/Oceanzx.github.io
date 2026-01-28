<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
body {
    margin:0;
    font-family: Arial, sans-serif;
    background:black;
    color:white;
    overflow-x:hidden;
}
/* PARTICLES */
.dot {
    position:fixed;
    width:3px;
    height:3px;
    background:white;
    border-radius:50%;
    opacity:0.8;
    animation:float linear infinite;
}
@keyframes float {0%{transform:translateY(-10vh)}100%{transform:translateY(120vh)}}

/* HEADER */
header {text-align:center; padding:20px;}
header h1 {font-size:3rem; font-weight:bold; margin:0;}
header p {margin:0; font-size:1.2rem; color:#ccc;}

/* GRID */
.grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:20px;
    margin:20px;
}

/* CARD */
.card {
    position:relative;
    background:none;
    text-align:center;
    border-radius:20px;
    padding:10px;
    cursor:pointer;
    transition:transform 0.2s, box-shadow 0.2s;
}
.card:hover {
    transform:translateY(-5px);
    box-shadow:0 0 15px rgba(255,255,255,0.2);
}
.card img {
    width:150px;
    height:150px;
    object-fit:contain;
    border-radius:20px; /* soft corners */
    transition:transform 0.2s;
}
.card img:hover {transform:scale(1.05);}
.card h3 {
    margin:8px 0 4px 0;
    font-weight:bold;
    color:white;
    -webkit-text-stroke: 1px black;
}
.card .price {margin:0; font-weight:bold;}
.card .stock {font-size:0.85rem; color:#ff5555;}
.btn {
    background:white;
    color:black;
    padding:6px 12px;
    border-radius:12px;
    font-weight:bold;
    cursor:pointer;
    border:none;
    margin-top:5px;
}
.btn:disabled {opacity:0.5; cursor:not-allowed;}

/* CART */
#cart {
    position:fixed;
    top:20px;
    right:20px;
    width:280px;
    max-height:80vh;
    overflow-y:auto;
    background:#111;
    border-radius:20px;
    padding:15px;
    box-shadow:0 0 20px rgba(255,255,255,0.3);
}
#cart h3 {margin-top:0;}
.cart-item {display:flex; justify-content:space-between; margin:5px 0;}
.cart-item span:first-child {cursor:pointer; color:red;}
.cart-total {margin-top:10px; font-weight:bold;}

/* SECTIONS */
section {margin:20px;}
section h2 {text-align:center; margin-bottom:10px;}

/* SCROLLBAR */
#cart::-webkit-scrollbar {width:8px;}
#cart::-webkit-scrollbar-thumb {background:#fff; border-radius:4px;}
</style>
</head>
<body>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted • Discord Checkout</p>
</header>

<section>
<h2>Pets</h2>
<div class="grid" id="pets-grid"></div>
</section>

<section>
<h2>Eggs</h2>
<div class="grid" id="eggs-grid"></div>
</section>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout</button>
</div>

<script>
// PARTICLES - FAST WHITE DOTS
for(let i=0;i<150;i++){
    let dot=document.createElement('div');
    dot.className='dot';
    dot.style.left=Math.random()*100+'vw';
    dot.style.animationDuration=(2+Math.random()*4)+'s'; // faster speed
    document.body.appendChild(dot);
}

// DATA
let cart=JSON.parse(localStorage.getItem("oceanzx-cart"))||[];

// PETS
let pets=[
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:5},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:5},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:5},
{name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769419308180-be119059-935c-4323-8d8a-2d0e5958128c.png",stock:5},
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
{name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15},
{name:"Aussie Egg",price:10,img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png",stock:15}
];

// RENDER
function renderItems(){
    const petsGrid=document.getElementById('pets-grid');
    const eggsGrid=document.getElementById('eggs-grid');
    petsGrid.innerHTML='';
    eggsGrid.innerHTML='';
    pets.forEach(item=>{
        const card=document.createElement('div');
        card.className='card';
        card.innerHTML=`<img src="${item.img}"><h3>${item.name}</h3><div class="price">$${item.price}</div><div class="stock" data-stock="${item.name}">Stock: ${item.stock}</div><button class="btn" onclick="addToCart('${item.name}',${item.price})">Add to Cart</button>`;
        petsGrid.appendChild(card);
    });
    eggs.forEach(item=>{
        const card=document.createElement('div');
        card.className='card';
        card.innerHTML=`<img src="${item.img}"><h3>${item.name}</h3><div class="price">$${item.price}</div><div class="stock" data-stock="${item.name}">Stock: ${item.stock}</div><button class="btn" onclick="addToCart('${item.name}',${item.price})">Add to Cart</button>`;
        eggsGrid.appendChild(card);
    });
}

// CART FUNCTIONS
function findItem(name){return pets.concat(eggs).find(i=>i.name===name);}
function addToCart(name,price){
    const item=findItem(name);
    if(!item||item.stock<=0) return;
    cart.push({name,price});
    item.stock--;
    updateStock(name);
    renderCart();
}
function updateStock(name){
    const item=findItem(name);
    const stockEl=document.querySelector(`[data-stock="${name}"]`);
    const btn=document.querySelector(`[onclick*="${name}"]`);
    if(item.stock<=0){stockEl.innerText="❌ SOLD OUT"; btn.disabled=true;}
    else stockEl.innerText="Stock: "+item.stock;
}
function renderCart(){
    const itemsEl=document.getElementById('cart-items');
    itemsEl.innerHTML='';
    let total=0;
    cart.forEach((i,idx)=>{
        total+=i.price;
        itemsEl.innerHTML+=`<div class="cart-item"><span onclick="removeFromCart(${idx})">❌</span><span>${i.name}</span><span>$${i.price}</span></div>`;
    });
    document.getElementById('total').innerText=total.toFixed(2);
    localStorage.setItem("oceanzx-cart",JSON.stringify(cart));
}
function removeFromCart(idx){
    const removed=cart.splice(idx,1)[0];
    const item=findItem(removed.name);
    if(item) item.stock++;
    updateStock(removed.name);
    renderCart();
}

// CHECKOUT DISCORD
function checkout(){
    if(cart.length===0){alert("Cart empty"); return;}
    let total=0;
    let orderText="🛒 Oceanzx Order\n";
    cart.forEach(i=>{
        orderText+=`${i.name} - $${i.price}\n`; 
        total+=i.price;
    });
    orderText+="\n💰 Total: $"+total.toFixed(2);
    navigator.clipboard.writeText(orderText);
    window.open("https://discord.com/users/1455058787257024512","_blank");
    cart=[]; renderCart();
}

renderItems(); renderCart();
</script>
</body>
</html>
