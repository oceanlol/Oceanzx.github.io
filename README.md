<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<meta name="description" content="Oceanzx Adopt Me Shop – Fast delivery, trusted trades, instant Discord checkout.">

<style>
:root {
    --accent:#ffffff;
    --bg:#000000;
    --card:#111111;
    --text:#e0e0e0;
}
*{box-sizing:border-box;}
body{margin:0;font-family:Arial,sans-serif;background:var(--bg);color:var(--text);overflow-x:hidden;}

/* Header */
header{text-align:center;padding:30px 20px;background:#111;}
header h1{margin:0;font-size:3rem;color:var(--accent);}
header p{color:#ccc;font-size:1.2rem;margin-top:6px;}

/* Container */
.container{max-width:1200px;margin:20px auto;padding:20px;}

/* Grid */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:20px;}

/* Card */
.card{background:var(--card);padding:15px;border-radius:15px;text-align:center;transition:0.3s;overflow:hidden;}
.card img{width:150px;height:150px;object-fit:cover;border-radius:12px;margin-bottom:10px;}
.card:hover{transform:translateY(-5px);box-shadow:0 0 15px #fff;}
.card h3{margin:0 0 8px;font-size:1rem;}
.card .price{color:#aaa;font-weight:bold;}
.card .stock{font-size:0.8rem;color:#ff4d4d;margin:4px 0;}

/* Button */
.btn{background:#333;color:#fff;border:none;padding:8px 16px;border-radius:12px;font-weight:bold;cursor:pointer;transition:0.3s;}
.btn:hover{background:#555;transform:scale(1.05);}
.btn:disabled{background:#444;cursor:not-allowed;}

/* Cart */
#cart{position:fixed;top:20px;right:20px;width:300px;background:#111;border-radius:12px;padding:15px;box-shadow:0 0 20px #fff;max-height:70vh;overflow-y:auto;z-index:999;}
#cart h3{margin:0 0 10px;font-size:1.2rem;}
.cart-item{display:flex;justify-content:space-between;margin:6px 0;font-size:0.9rem;}
.cart-item span:first-child{color:red;cursor:pointer;}
.cart-total{margin-top:10px;font-weight:bold;}
</style>
</head>
<body>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Adopt Me • Clean • Trusted</p>
<p>👀 <span id="viewers">27</span> people viewing</p>
</header>

<div class="container">
<h2>🥚 Eggs</h2>
<div class="grid" id="eggs-grid"></div>

<h2>🔥 Pets</h2>
<div class="grid" id="pets-grid"></div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout</button>
</div>

<script>
// Data
let cart = [];
const items = [
    {name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png",stock:15,type:"egg"},
    {name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png",stock:15,type:"egg"},
    {name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png",stock:15,type:"egg"},
    {name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15,type:"egg"},
    {name:"Aussie Egg",price:10,img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png",stock:15,type:"egg"},

    // Pets
    {name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:5,type:"pet"},
    {name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:5,type:"pet"},
    {name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:5,type:"pet"},
    {name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png",stock:5,type:"pet"},
    {name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",stock:5,type:"pet"},
    {name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",stock:5,type:"pet"},
    {name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",stock:5,type:"pet"}
];

// Render function
function renderItems(){
    const eggsGrid = document.getElementById("eggs-grid");
    const petsGrid = document.getElementById("pets-grid");
    eggsGrid.innerHTML=""; petsGrid.innerHTML="";
    items.forEach(it=>{
        const card = document.createElement("div");
        card.className="card";
        card.innerHTML=`
            <img src="${it.img}" alt="${it.name}">
            <h3>${it.name}</h3>
            <div class="price">$${it.price}</div>
            <div class="stock" data-stock="${it.name}">Stock: ${it.stock}</div>
            <button class="btn" ${it.stock===0?'disabled':''} onclick="addToCart('${it.name}')">Add to Cart</button>
        `;
        if(it.type==="egg") eggsGrid.appendChild(card);
        else petsGrid.appendChild(card);
    });
}

// Cart functions
function findItem(name){return items.find(i=>i.name===name);}
function addToCart(name){
    const it = findItem(name);
    if(!it || it.stock<=0) return;
    cart.push({name,price:it.price,img:it.img});
    it.stock--;
    renderItems(); renderCart();
}
function removeFromCart(idx){
    const item = cart.splice(idx,1)[0];
    const it = findItem(item.name);
    if(it) it.stock++;
    renderItems(); renderCart();
}
function renderCart(){
    const el = document.getElementById("cart-items");
    el.innerHTML="";
    let total=0;
    cart.forEach((i,idx)=>{
        total+=i.price;
        el.innerHTML+=`<div class="cart-item">
            <span onclick="removeFromCart(${idx})">❌</span>
            <span>${i.name}</span>
            <span>$${i.price}</span>
        </div>`;
    });
    document.getElementById("total").innerText=total.toFixed(2);
}

// Checkout
function checkout(){
    if(cart.length===0) return alert("Cart is empty");
    let text="🛒 Oceanzx Order\n";
    let total=0;
    cart.forEach(i=>{
        text+=`• ${i.name} - $${i.price}\n`;
        total+=i.price;
    });
    text+=`\n💰 Total: $${total.toFixed(2)}`;
    navigator.clipboard.writeText(text);
    alert("Cart copied! Send to Discord in buying ticket.");
    window.open("https://discord.gg/sv6tRJBR5G","_blank");
    cart=[];
    renderCart();
}

// Initialize
renderItems();
</script>
</body>
</html>
