<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OCEANZX • Adopt Me Shop</title>
<style>
/* RESET */
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Inter,Arial,sans-serif;background:#000;color:#fff}

/* HEADER */
header{padding:28px 20px;border-bottom:1px solid #1a1a1a;text-align:center}
header h1{letter-spacing:4px;font-size:32px}
header p{margin-top:8px;font-size:14px;opacity:.7}
#viewing{margin-top:10px;font-size:13px;opacity:.6}

/* LAYOUT */
main{max-width:1200px;margin:0 auto;padding:30px}
.section-title{font-size:18px;letter-spacing:2px;margin:40px 0 20px;border-left:4px solid #fff;padding-left:12px}

/* GRID */
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:28px}

/* PRODUCT CARD */
.card{background:#0b0b0b;border:1px solid #1a1a1a;border-radius:18px;padding:18px;display:flex;flex-direction:column;align-items:center;transition:.25s}
.card:hover{transform:translateY(-6px);border-color:#fff}

/* IMAGE FIX */
.card-img{width:100%;aspect-ratio:1/1;background:#050505;border-radius:14px;display:flex;align-items:center;justify-content:center;overflow:hidden;margin-bottom:16px}
.card-img img{width:100%;height:100%;object-fit:contain;padding:10px}

/* TEXT */
.card h3{font-size:16px;margin-bottom:6px;text-align:center}
.price{font-size:14px;opacity:.8;margin-bottom:4px}
.stock{font-size:12px;opacity:.5;margin-bottom:14px}

/* BUTTON */
button{width:100%;padding:12px;border-radius:12px;border:1px solid #fff;background:#fff;color:#000;font-weight:bold;cursor:pointer;transition:.25s}
button:hover{background:#000;color:#fff}
button:disabled{opacity:.3;border-color:#333;cursor:not-allowed}

/* CART */
#cart{position:fixed;right:24px;top:120px;width:300px;background:#0b0b0b;border:1px solid #1a1a1a;border-radius:20px;padding:16px}
#cart h2{text-align:center;margin-bottom:10px;font-size:16px}
.cart-item{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid #1a1a1a}
.cart-item img{width:36px;height:36px;object-fit:contain;background:#000;border-radius:8px;padding:4px}
.cart-item span{flex:1;font-size:13px}
.remove{font-size:12px;cursor:pointer;opacity:.6}
#total{margin-top:12px;text-align:center;font-weight:bold}
#checkout{margin-top:12px}

/* DEV BUTTON */
#devBtn{position:fixed;right:20px;bottom:20px;width:44px;height:44px;border-radius:50%;background:#111;border:1px solid #333;display:flex;align-items:center;justify-content:center;cursor:pointer;font-weight:bold}
</style>
</head>
<body>

<header>
<h1>OCEANZX</h1>
<p>Adopt Me • Clean • Trusted</p>
<div id="viewing">👀 27 people viewing</div>
</header>

<main>
<h2 class="section-title">🥚 EGGS</h2>
<div class="grid" id="eggs"></div>

<h2 class="section-title">🐾 PETS</h2>
<div class="grid" id="pets"></div>
</main>

<div id="cart">
<h2>Cart</h2>
<div id="cartItems"></div>
<div id="total">Total: $0.00</div>
<button id="checkout">Checkout</button>
<p style="font-size:11px;opacity:.6;text-align:center;margin-top:8px">Cash App: $Bananaboy723</p>
</div>

<div id="devBtn">O</div>

<script>
const items=[
{name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769340250503-3d3f2972-9914-4529-9abd-abaf9b370d22.png",stock:0,type:"egg"},
{name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:3,type:"pet"},
{name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg",stock:2,type:"pet"},
{name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png",stock:1,type:"pet"},
{name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png",stock:2,type:"pet"},
{name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg",stock:1,type:"pet"},
{name:"Snow Owl Fly Ride",price:2.5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg",stock:4,type:"pet"}
];

let cart=[];
const eggs=document.getElementById('eggs');
const pets=document.getElementById('pets');

function render(){eggs.innerHTML="";pets.innerHTML="";items.forEach(i=>{const card=document.createElement('div');card.className='card';card.innerHTML=`<div class="card-img"><img src="${i.img}"></div><h3>${i.name}</h3><div class="price">$${i.price}</div><div class="stock">Stock: ${i.stock}</div><button ${i.stock===0?'disabled':''}>Add to Cart</button>`;card.querySelector('button').onclick=()=>add(i);(i.type==='egg'?eggs:pets).appendChild(card);});}

function add(i){cart.push(i);i.stock--;render();renderCart();}
function renderCart(){const c=document.getElementById('cartItems');c.innerHTML="";let t=0;cart.forEach((i,idx)=>{t+=i.price;const d=document.createElement('div');d.className='cart-item';d.innerHTML=`<img src="${i.img}"><span>${i.name}</span><span class="remove" onclick="remove(${idx})">✕</span>`;c.appendChild(d);});document.getElementById('total').innerText=`Total: $${t.toFixed(2)}`;}
function remove(i){cart.splice(i,1);renderCart();}

render();
</script>
</body>
</html>
