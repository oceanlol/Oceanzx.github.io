<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
:root {
    --bg:#000;
    --dot:#fff;
    --cart-bg:#121212;
    --cart-border:#fff;
    --text:#fff;
    --btn-bg:#000;
    --btn-border:#fff;
}
*{box-sizing:border-box;margin:0;padding:0;font-family:Arial, sans-serif;}
body{background:var(--bg);color:var(--text);overflow-x:hidden;}

/* PARTICLES */
.dot{position:fixed;width:2px;height:2px;background:var(--dot);border-radius:50%;animation:fall linear infinite;}
@keyframes fall{0%{transform:translateY(-10vh)}100%{transform:translateY(120vh)}}

/* HEADER */
header{text-align:center;padding:30px;}
header h1{font-size:3rem;font-weight:bold;color:#fff;text-shadow:1px 1px 0 #000;}
header p{margin-top:5px;color:#ccc;font-size:1.2rem;}

/* GRID */
.container{max-width:1200px;margin:0 auto;padding:20px;display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:20px;}
.card{background:#000;border:2px solid #fff;border-radius:20px;padding:10px;text-align:center;transition:0.3s;cursor:pointer;}
.card img{width:100%;height:180px;object-fit:contain;margin-bottom:10px;}
.card h3{color:#fff;font-weight:bold;font-size:1.1rem;margin-bottom:5px;}
.card .price{color:#fff;font-weight:bold;margin-bottom:5px;}
.card .stock{color:#fff;font-size:0.9rem;margin-bottom:5px;}
.card button{background:var(--btn-bg);color:var(--text);border:2px solid var(--btn-border);padding:5px 10px;border-radius:10px;font-weight:bold;cursor:pointer;transition:0.2s;}
.card button:hover{transform:scale(1.05);}

/* CART */
#cart{position:fixed;top:50px;right:20px;width:300px;background:var(--cart-bg);border:2px solid var(--cart-border);border-radius:20px;padding:15px;max-height:80vh;overflow-y:auto;z-index:999;}
#cart h3{font-weight:bold;margin-bottom:10px;text-align:center;}
.cart-item{display:flex;justify-content:space-between;margin-bottom:5px;font-size:0.9rem;}
.cart-total{font-weight:bold;margin-top:10px;text-align:center;}
#checkout-btn{width:100%;padding:10px;border-radius:12px;border:2px solid var(--btn-border);background:var(--btn-bg);color:var(--text);font-weight:bold;cursor:pointer;margin-top:10px;transition:0.2s;}
#checkout-btn:hover{transform:scale(1.05);}
</style>
</head>
<body>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Adopt Me • Clean • Trusted</p>
<p id="viewing-count">👀 27 people viewing</p>
</header>

<div class="container" id="pets-grid"></div>
<div class="container" id="eggs-grid"></div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cart-items"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button id="checkout-btn" onclick="checkout()">Checkout via CashApp</button>
</div>

<script>
// PARTICLES
for(let i=0;i<100;i++){
    let dot=document.createElement('div');
    dot.className='dot';
    dot.style.left=Math.random()*100+'vw';
    dot.style.animationDuration=(3+Math.random()*5)+'s';
    dot.style.width=(1+Math.random()*2)+'px';
    dot.style.height=dot.style.width;
    document.body.appendChild(dot);
}

// DATA
let cart = [];
let pets=[
{name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:5},
{name:"Reindeer Fly Ride",price:2.3,img:"https://image2url.com/r2/default/images/1769340396217-88705f92-43c7-4f07-97ca-2b5d1279ace3.png",stock:5},
{name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:5},
{name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg",stock:5},
{name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png",stock:5},
{name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png",stock:5},
{name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg",stock:5},
{name:"Snow Owl Fly Ride",price:2.5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg",stock:5},
// NEW PETS
{name:"Strawberry Shortcake Bat Dragon Fly Ride",price:24,img:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png",stock:5},
{name:"Cow Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png",stock:5},
{name:"Chocolate Chip Bat Dragon Fly Ride",price:20,img:"https://image2url.com/r2/default/images/1769417573051-1675be6f-08e2-46bc-b60f-3f8f478db80a.png",stock:5},
{name:"Dragonfruit Fox",price:12.5,img:"https://image2url.com/r2/default/images/1769417684237-e455a114-a17c-49ba-8c95-ee41c1698ec6.png",stock:5},
{name:"Unicorn",price:3.25,img:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png",stock:5},
{name:"German Shepherd Fly Ride",price:11.2,img:"https://image2url.com/r2/default/images/1769417898335-95161f79-12d0-4e89-a55f-a0af98128192.png",stock:5},
{name:"Turtle Fly Ride",price:22.1,img:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png",stock:5},
];

let eggs=[
{name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769418420566-8274a492-a6e0-42d4-a4c8-018c13c65bae.png",stock:15},
{name:"Retired Egg",price:2,img:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png",stock:15},
{name:"Moon Egg",price:1.25,img:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png",stock:15},
{name:"Royal Egg",price:5,img:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png",stock:15},
{name:"Aussie Egg",price:10,img:"https://image2url.com/r2/default/images/1769418468586-a61ac3ef-3b69-41e6-af48-c7f2c8433262.png",stock:15},
];

// RENDER
function renderCards(container,arr){
    container.innerHTML="";
    arr.forEach((item)=>{
        const card=document.createElement('div');
        card.className='card';
        card.innerHTML=`<img src="${item.img}" alt="${item.name}"><h3>${item.name}</h3><div class="price">$${item.price}</div><div class="stock">Stock: ${item.stock}</div><button onclick="addToCart('${item.name}')">Add to Cart</button>`;
        container.appendChild(card);
    });
}
renderCards(document.getElementById('pets-grid'),pets);
renderCards(document.getElementById('eggs-grid'),eggs);

// CART LOGIC
function addToCart(name){
    let item=pets.find(i=>i.name===name) || eggs.find(i=>i.name===name);
    if(item && item.stock>0){
        cart.push({...item});
        item.stock--;
        renderCards(document.getElementById('pets-grid'),pets);
        renderCards(document.getElementById('eggs-grid'),eggs);
        renderCart();
    }else{
        alert("Out of stock!");
    }
}

function renderCart(){
    const cartEl=document.getElementById('cart-items');
    cartEl.innerHTML="";
    let total=0;
    cart.forEach((c,i)=>{
        total+=c.price;
        cartEl.innerHTML+=`<div class="cart-item"><span onclick="removeFromCart(${i})">❌</span> <span>${c.name}</span> <span>$${c.price}</span></div>`;
    });
    document.getElementById('total').innerText=total.toFixed(2);
}

function removeFromCart(i){
    let item=cart[i];
    let original=pets.find(p=>p.name===item.name)||eggs.find(e=>e.name===item.name);
    if(original) original.stock++;
    cart.splice(i,1);
    renderCart();
    renderCards(document.getElementById('pets-grid'),pets);
    renderCards(document.getElementById('eggs-grid'),eggs);
}

// CHECKOUT
function checkout(){
    if(cart.length==0){alert("Cart empty!"); return;}
    let text="🛒 Oceanzx Order:\n";
    let total=0;
    cart.forEach(i=>{
        text+=`• ${i.name} - $${i.price}\n`;
        total+=i.price;
    });
    text+=`\n💰 Total: $${total.toFixed(2)}\n💵 Send payment to CashApp: $Bananaboy723`;
    alert("Copy your cart:\n"+text);
    navigator.clipboard.writeText(text);
    cart=[];
    renderCart();
    renderCards(document.getElementById('pets-grid'),pets);
    renderCards(document.getElementById('eggs-grid'),eggs);
}

renderCart();
</script>
</body>
</html>
