<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx • Adopt Me Shop</title>
<meta name="description" content="Oceanzx Adopt Me Shop — clean, trusted, instant checkout via Discord.">

<style>
/* =====================
   CLEAN BLACK & WHITE UI
   ===================== */
:root{
  --bg:#0a0a0a;
  --bg-soft:#111;
  --card:#151515;
  --border:#1f1f1f;
  --text:#ffffff;
  --muted:#9a9a9a;
  --accent:#ffffff;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Inter,Segoe UI,Arial,sans-serif;
  background:var(--bg);
  color:var(--text);
}

/* LAYOUT */
.wrapper{max-width:1200px;margin:0 auto;padding:32px}

/* HEADER */
header{
  display:flex;justify-content:space-between;align-items:center;
  border-bottom:1px solid var(--border);padding-bottom:24px;margin-bottom:32px
}
header h1{margin:0;font-size:1.8rem;letter-spacing:1px}
header span{color:var(--muted);font-size:.9rem}

/* VIEW COUNTER */
#viewing{font-size:.85rem;color:var(--muted)}

/* SECTIONS */
.section{margin-bottom:56px}
.section h2{font-size:1.4rem;margin-bottom:18px;letter-spacing:.5px}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
  gap:22px
}

/* PRODUCT CARD */
.card{
  background:var(--card);
  border:1px solid var(--border);
  border-radius:14px;
  padding:16px;
  transition:.25s
}
.card:hover{transform:translateY(-4px)}
.card img{
  width:100%;height:180px;object-fit:cover;
  border-radius:10px;margin-bottom:12px
}
.card h3{margin:0;font-size:1rem;font-weight:500}
.price{color:var(--muted);font-size:.9rem;margin:6px 0}
.stock{font-size:.75rem;color:#777}

.card button{
  margin-top:10px;width:100%;
  background:#fff;color:#000;
  border:none;border-radius:10px;
  padding:10px;font-weight:600;cursor:pointer
}
.card button:disabled{opacity:.4;cursor:not-allowed}

/* CART */
#cart{
  position:fixed;right:24px;top:24px;
  width:300px;background:var(--bg-soft);
  border:1px solid var(--border);
  border-radius:16px;padding:16px
}
#cart h3{margin:0 0 12px 0;font-size:1.1rem}
.cart-item{
  display:grid;grid-template-columns:1fr auto;
  gap:6px;font-size:.85rem;margin-bottom:6px
}
.cart-item small{color:var(--muted)}
.cart-total{margin-top:10px;font-weight:600}

#checkoutBtn{
  width:100%;margin-top:12px;
  background:#fff;color:#000;
  border:none;border-radius:12px;
  padding:12px;font-weight:700;cursor:pointer
}

/* UPDATES PANEL */
#updates{
  margin-top:32px;
  border-top:1px solid var(--border);
  padding-top:16px
}
#updates h4{margin:0 0 8px 0}

/* DEV MODE */
#devBtn{
  position:fixed;left:14px;bottom:14px;
  width:42px;height:42px;border-radius:50%;
  background:#fff;color:#000;
  display:flex;align-items:center;justify-content:center;
  font-weight:800;cursor:pointer
}
#devPanel{
  display:none;position:fixed;left:70px;bottom:14px;
  width:260px;background:#111;border:1px solid #333;
  border-radius:12px;padding:14px
}
#devPanel textarea{width:100%;height:80px;background:#000;color:#fff;border:1px solid #333}
#devPanel button{margin-top:8px;width:100%}
</style>
</head>
<body>

<div class="wrapper">
<header>
  <div>
    <h1>OCEANZX</h1>
    <span>Adopt Me • Clean • Trusted</span>
  </div>
  <div id="viewing">👀 14 people viewing</div>
</header>

<section class="section">
<h2>🥚 Eggs</h2>
<div class="grid" id="eggs"></div>
</section>

<section class="section">
<h2>🐾 Pets</h2>
<div class="grid" id="pets"></div>
</section>

<section id="updates">
<h4>📢 Updates</h4>
<p id="updateText">New clean black & white UI launched.</p>
</section>
</div>

<div id="cart">
<h3>🛒 Cart</h3>
<div id="cartItems"></div>
<div class="cart-total">Total: $<span id="total">0.00</span></div>
<button id="checkoutBtn">Checkout</button>
<p style="font-size:.7rem;color:#777;margin-top:6px">Cash App: <b>$Bananaboy723</b></p>
</div>

<div id="devBtn">O</div>
<div id="devPanel">
<b>Dev Mode</b>
<textarea id="devMsg" placeholder="Message to display..."></textarea>
<button onclick="pushUpdate()">Push Update</button>
</div>

<script>
/* DATA */
const items=[
 {name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769340250503-3d3f2972-9914-4529-9abd-abaf9b370d22.png",type:"egg",stock:3},
 {name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",type:"pet",stock:3},
 {name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg",type:"pet",stock:2},
 {name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png",type:"pet",stock:1},
 {name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png",type:"pet",stock:2},
 {name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg",type:"pet",stock:1},
 {name:"Snow Owl Fly Ride",price:2.5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg",type:"pet",stock:4}
];

let cart=[];

/* RENDER */
function render(){
  eggs.innerHTML=""; pets.innerHTML="";
  items.forEach(i=>{
    const c=document.createElement('div');
    c.className='card';
    c.innerHTML=`<img src="${i.img}"><h3>${i.name}</h3><div class="price">$${i.price}</div><div class="stock">Stock: ${i.stock}</div><button ${i.stock<=0?'disabled':''}>Add to Cart</button>`;
    c.querySelector('button').onclick=()=>add(i);
    (i.type==='egg'?eggs:pets).appendChild(c);
  });
}

function add(i){if(i.stock<=0)return;cart.push(i);i.stock--;render();renderCart();new Audio('https://assets.mixkit.co/sfx/preview/mixkit-select-click-1109.mp3').play();}

function renderCart(){
  cartItems.innerHTML=''; let t=0;
  cart.forEach(p=>{t+=p.price;cartItems.innerHTML+=`<div class='cart-item'><div>${p.name}<br><small>$${p.price}</small></div></div>`});
  total.innerText=t.toFixed(2);
}

checkoutBtn.onclick=()=>{
  if(!cart.length)return alert('Cart empty');
  const id=Math.floor(Math.random()*900000+100000);
  let text=`Order ${id}\n`;
  cart.forEach(p=>text+=`• ${p.name} $${p.price}\n`);
  text+=`Total: $${total.innerText}`;
  navigator.clipboard.writeText(text);
  window.open('https://discord.gg/sv6tRJBR5G','_blank');
  cart=[];renderCart();
};

/* DEV MODE */
devBtn.onclick=()=>{
  const p=prompt('Password');
  if(p==='Keebs')devPanel.style.display='block';
};
function pushUpdate(){updateText.innerText=devMsg.value;}

/* VIEW COUNTER */
setInterval(()=>{
  viewing.innerText=`👀 ${Math.floor(Math.random()*20+8)} people viewing`;
},4000);

render();
</script>
</body>
</html>
