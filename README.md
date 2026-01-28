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
    transition:transform 0.2s;
}
.card:hover {transform:translateY(-5px);}
.card img {
    width:150px;
    height:150px;
    object-fit:contain;
    filter:brightness(0) invert(1); /* black silhouette + invert */
    position:relative;
}
.wave {
    position:absolute;
    width:80px;
    height:8px;
    background:white;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%) rotate(-15deg);
    border-radius:4px;
}
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
<p>Fast delivery • Trusted • CashApp Only</p>
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
// PARTICLES
for(let i=0;i<100;i++){
    const dot = document.createElement('div');
    dot.className='dot';
    dot.style.left=Math.random()*100+'vw';
    dot.style.animationDuration=(5+Math.random()*10)+'s';
    document.body.appendChild(dot);
}

// ITEMS DATA
let cart = [];
let pets = [
    {name:"Axolotl Fly Ride", price:2, img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png", stock:5},
    {name:"Cerberus Fly Ride", price:3, img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg", stock:5},
    {name:"Dango Penguins", price:10, img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png", stock:5},
    {name:"Neon Sneak Weasel (5)", price:12, img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png", stock:5},
    {name:"Ride Sakura Spirit", price:8, img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg", stock:5},
    {name:"Snow Owl Fly Ride", price:2.5, img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg", stock:5},
    // New pets
    {name:"Strawberry Shortcake Bat Dragon Fly Ride", price:24, img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png", stock:5},
    {name:"Cow Fly Ride", price:20, img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png", stock:5},
    {name:"Chocolate Chip Bat Dragon Fly Ride", price:20, img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png", stock:5},
    {name:"Dragonfruit Fox", price:12.5, img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png", stock:5},
    {name:"Unicorn", price:3.25, img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png", stock:5},
    {name:"German Shepherd Fly Ride", price:11.2, img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png", stock:5},
    {name:"Turtle Fly Ride", price:22.1, img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png", stock:5}
];
let eggs = [
    {name:"Crystal Egg", price:1, img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png", stock:15},
    {name:"Retired Egg", price:2, img:"https://image2url.com/r2/default/images/1769418455991-0cd50c08-7af1-433f-8438-1ff08827d293.png", stock:15},
    {name:"Moon Egg", price:1.25, img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png", stock:15},
    {name:"Royal Egg", price:5, img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png", stock:15},
    {name:"Aussie Egg", price:10, img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png", stock:15}
];

// RENDER
function renderGrid(items, gridId){
    const grid = document.getElementById(gridId);
    grid.innerHTML="";
    items.forEach((it, idx)=>{
        const card = document.createElement('div');
        card.className='card';
        card.innerHTML = `
            <div style="position:relative;">
                <img src="${it.img}" alt="${it.name}">
                <div class="wave"></div>
            </div>
            <h3>${it.name}</h3>
            <div class="price">$${it.price}</div>
            <div class="stock" id="stock-${gridId}-${idx}">Stock: ${it.stock}</div>
            <button class="btn" onclick="addToCart('${gridId}',${idx})">Add to Cart</button>
        `;
        grid.appendChild(card);
    });
}
function updateStock(gridId, idx){
    const item = (gridId==='pets-grid'?pets:eggs)[idx];
    document.getElementById(`stock-${gridId}-${idx}`).innerText=`Stock: ${item.stock}`;
}
function addToCart(gridId, idx){
    const item = (gridId==='pets-grid'?pets:eggs)[idx];
    if(item.stock<=0) return alert('Out of stock!');
    cart.push({name:item.name,price:item.price});
    item.stock--;
    updateStock(gridId, idx);
    renderCart();
}
function renderCart(){
    const cartEl = document.getElementById('cart-items');
    cartEl.innerHTML="";
    let total=0;
    cart.forEach((c,i)=>{
        total+=c.price;
        const div = document.createElement('div');
        div.className='cart-item';
        div.innerHTML=`<span onclick="removeFromCart(${i})">❌</span><span>${c.name}</span><span>$${c.price}</span>`;
        cartEl.appendChild(div);
    });
    document.getElementById('total').innerText=total.toFixed(2);
}
function removeFromCart(idx){
    const item = cart.splice(idx,1)[0];
    // restore stock
    pets.forEach(p=>{if(p.name===item.name)p.stock++;});
    eggs.forEach(e=>{if(e.name===item.name)e.stock++;});
    renderCart(); renderGrid(pets,'pets-grid'); renderGrid(eggs,'eggs-grid');
}
function checkout(){
    if(cart.length===0) return alert("Cart empty!");
    let total=0;
    let text="🛒 Oceanzx Order\n";
    cart.forEach(c=>{text+=`• ${c.name} - $${c.price}\n`; total+=c.price;});
    text+=`\n💰 Total: $${total.toFixed(2)}`;
    navigator.clipboard.writeText(text);
    alert("Cart copied! Send payment via CashApp $Bananaboy723");
    cart=[]; renderCart(); renderGrid(pets,'pets-grid'); renderGrid(eggs,'eggs-grid');
}

// INIT
renderGrid(pets,'pets-grid');
renderGrid(eggs,'eggs-grid');
renderCart();
</script>
</body>
</html>
