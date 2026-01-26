<!DOCTYPE html>
<!-- FULL FILE – OCEANZX ADOPT ME SHOP (PC VERSION) -->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>

<style>
/* ===================== ROOT ===================== */
:root{
--accent:#0a84ff;
--bg:#0b0b0b;
--card:#151515;
--text:#ffffff;
--good:#00ff99;
}
*{box-sizing:border-box}
body{
margin:0;
font-family:Segoe UI,Arial,sans-serif;
background:var(--bg);
color:var(--text);
overflow-x:hidden;
}

/* ===================== HEADER ===================== */
header{
text-align:center;
padding:40px 20px;
background:linear-gradient(180deg,#111,#000);
}
header h1{
font-size:2.8rem;
color:var(--accent);
text-shadow:0 0 12px #0a84ff;
}
header p{color:#aaa}

/* ===================== CONTAINER ===================== */
.container{
max-width:1200px;
margin:30px auto;
padding:30px;
background:#111;
border-radius:30px;
}

h2{text-align:center;margin:40px 0 20px}

/* ===================== GRID ===================== */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
gap:25px;
}
.card{
background:linear-gradient(180deg,var(--card),#0d0d0d);
border-radius:24px;
padding:18px;
text-align:center;
transition:.3s;
}
.card:hover{transform:translateY(-6px)}
.card img{
width:160px;
height:160px;
border-radius:20px;
object-fit:cover;
}
.price{margin-top:8px;font-weight:bold}
.stock{font-size:.8rem;color:#ff4d4d}
.btn{
margin-top:10px;
padding:10px 20px;
border:none;
border-radius:16px;
background:var(--accent);
color:white;
font-weight:bold;
cursor:pointer;
}
.btn:disabled{background:#444}

/* ===================== CART ===================== */
#cart{
position:fixed;
top:20px;
right:20px;
width:300px;
background:#111;
border-radius:24px;
padding:18px;
z-index:999;
}
#cart h3{text-align:center;margin-top:0}
.cart-item{
display:flex;
justify-content:space-between;
font-size:.9rem;
margin:6px 0;
}
.cart-total{margin-top:10px;font-weight:bold}

/* ===================== UPDATE PANEL ===================== */
#updatesBtn{
position:fixed;
bottom:20px;
left:20px;
background:var(--accent);
padding:10px 14px;
border-radius:14px;
cursor:pointer;
}
#updatesPanel{
display:none;
position:fixed;
bottom:80px;
left:20px;
width:320px;
background:#111;
border-radius:20px;
padding:16px;
}

/* ===================== DEV MODE ===================== */
#devBtn{
position:fixed;
right:10px;
bottom:50%;
background:#222;
border-radius:50%;
width:36px;
height:36px;
text-align:center;
line-height:36px;
font-weight:bold;
cursor:pointer;
}
#devPanel{
display:none;
position:fixed;
right:60px;
bottom:40%;
background:#111;
padding:18px;
border-radius:20px;
width:260px;
}

/* ===================== VIEW COUNTER ===================== */
#viewing{
text-align:center;
color:#aaa;
margin-bottom:10px;
}
</style>
</head>
<body>

<header>
<h1>Oceanzx Adopt Me Shop</h1>
<p>Fast delivery • Trusted trades • Discord checkout</p>
</header>

<div class="container">
<div id="viewing">👀 17 people viewing this</div>

<h2>Pets & Eggs</h2>
<div class="grid" id="shop"></div>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cartItems"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button class="btn" onclick="checkout()">Checkout</button>
<p style="font-size:.75rem;color:#aaa">Pay with Cash App: <b>$Bananaboy723</b></p>
</div>

<div id="updatesBtn" onclick="toggleUpdates()">🆕 Updates</div>
<div id="updatesPanel">
<b>Latest Updates</b><br><br>
• Cart system upgraded<br>
• Discount codes added<br>
• Dev mode added<br>
• Checkout copy improved<br>
</div>

<div id="devBtn" onclick="devLogin()">O</div>
<div id="devPanel">
<b>DEV MODE</b><br><br>
<input id="devText" placeholder="Banner text" style="width:100%"><br><br>
<button class="btn" onclick="pushText()">Push Text</button>
</div>

<audio id="addSound" src="https://cdn.pixabay.com/audio/2022/03/15/audio_2a2d10f8b5.mp3"></audio>

<script>
/* ===================== DATA ===================== */
let items=[
{name:"Snow Owl Fly Ride",price:2.5,stock:4,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg"},
{name:"Axolotl Fly Ride",price:2,stock:3,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png"}
];
let cart=[];

/* ===================== RENDER ===================== */
function render(){
const shop=document.getElementById('shop');
shop.innerHTML="";
items.forEach((i,idx)=>{
shop.innerHTML+=`
<div class="card">
<img src="${i.img}">
<h3>${i.name}</h3>
<div class="price">$${i.price}</div>
<div class="stock">Stock: ${i.stock}</div>
<button class="btn" ${i.stock<=0?'disabled':''} onclick="add(${idx})">Add to Cart</button>
</div>`;
});
}

function add(i){
if(items[i].stock<=0)return;
items[i].stock--;
cart.push(items[i]);
document.getElementById('addSound').play();
render();renderCart();
}

function renderCart(){
let el=document.getElementById('cartItems');
el.innerHTML="";let t=0;
cart.forEach(c=>{t+=c.price;el.innerHTML+=`<div class='cart-item'><span>${c.name}</span><span>$${c.price}</span></div>`});
document.getElementById('total').innerText=t.toFixed(2);
}

function checkout(){
if(!cart.length)return alert('Cart empty');
let id='OZX-'+Math.floor(Math.random()*900000+100000);
let txt=`Order ${id}\n`;
cart.forEach(i=>txt+=`• ${i.name} ($${i.price})\n`);
txt+=`Total: $${document.getElementById('total').innerText}`;
navigator.clipboard.writeText(txt);
alert('Copied! Screenshot cart and send in Discord ticket');
window.open('https://discord.gg/sv6tRJBR5G','_blank');
cart=[];renderCart();
}

/* ===================== EXTRAS ===================== */
function toggleUpdates(){
const p=document.getElementById('updatesPanel');
p.style.display=p.style.display==='block'?'none':'block';
}
function devLogin(){
const pass=prompt('Password');
if(pass==='Keebs')document.getElementById('devPanel').style.display='block';
}
function pushText(){
alert(document.getElementById('devText').value);
}

setInterval(()=>{
document.getElementById('viewing').innerText=`👀 ${Math.floor(Math.random()*15+10)} people viewing this`;
},4000);

render();
</script>
</body>
</html>
