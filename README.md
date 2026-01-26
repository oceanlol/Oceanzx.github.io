<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OCEANZX Adopt Me Shop</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:Inter,Arial,sans-serif}
body{background:#000;color:#fff}
header{padding:40px 20px;text-align:center;border-bottom:1px solid #1a1a1a}
header h1{font-size:36px;letter-spacing:4px}
header p{margin-top:8px;font-size:16px;opacity:.7}
#viewing{margin-top:10px;font-size:14px;opacity:.6}
main{max-width:1300px;margin:0 auto;padding:30px}
.section-title{font-size:20px;letter-spacing:2px;margin:40px 0 20px;border-left:4px solid #fff;padding-left:12px}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:28px}
.card{background:#0b0b0b;border:1px solid #1a1a1a;border-radius:18px;padding:18px;display:flex;flex-direction:column;align-items:center;transition:.25s;position:relative;overflow:hidden}
.card:hover{transform:translateY(-6px);border-color:#fff;box-shadow:0 0 20px rgba(255,255,255,.2)}
.card-img{width:100%;aspect-ratio:1/1;background:#050505;border-radius:14px;display:flex;align-items:center;justify-content:center;overflow:hidden;margin-bottom:16px}
.card-img img{width:100%;height:100%;object-fit:contain;padding:10px}
.card h3{font-size:16px;margin-bottom:6px;text-align:center}
.price{font-size:14px;opacity:.8;margin-bottom:4px}
.stock{font-size:12px;opacity:.5;margin-bottom:14px}
button{width:100%;padding:12px;border-radius:12px;border:1px solid #fff;background:#fff;color:#000;font-weight:bold;cursor:pointer;transition:.25s}
button:hover{background:#000;color:#fff}
button:disabled{opacity:.3;border-color:#333;cursor:not-allowed}
#cart{position:fixed;right:24px;top:120px;width:360px;background:#0b0b0b;border:2px solid #fff;border-radius:24px;padding:16px;box-shadow:0 0 30px rgba(255,255,255,.3)}
#cart h2{text-align:center;margin-bottom:12px;font-size:18px;letter-spacing:1px}
.cart-item{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid #1a1a1a;transition:.2s;position:relative}
.cart-item:hover{background:rgba(255,255,255,.05);border-radius:12px;transform:scale(1.02)}
.cart-item img{width:48px;height:48px;object-fit:contain;background:#000;border-radius:8px;padding:4px;flex-shrink:0}
.cart-item span{flex:1;font-size:14px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.remove{font-size:14px;cursor:pointer;opacity:.6;transition:.2s}
.remove:hover{color:red;opacity:1}
#total{margin-top:12px;text-align:center;font-weight:bold;font-size:16px}
#checkout{margin-top:12px;padding:12px;background:#fff;color:#000;border-radius:16px;border:none;font-weight:bold;cursor:pointer;width:100%;transition:.25s}
#checkout:hover{background:#000;color:#fff;transform:scale(1.05)}
#updates{position:fixed;left:20px;top:120px;width:300px;background:#0b0b0b;border:1px solid #1a1a1a;border-radius:16px;padding:12px;max-height:400px;overflow-y:auto;display:none}
#updates h3{margin-bottom:8px;text-align:center}
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
<div id="updates">
<h3>Latest Updates</h3>
<ul id="updateList"></ul>
</div>
<div id="devBtn">O</div>
<script>
const items=[
{name:"Crystal Egg",price:1,img:"https://image2url.com/r2/default/images/1769340250503-3d3f2972-9914-4529-9abd-abaf9b370d22.png",stock:0,type:"egg"},
{name:"Snow Owl NO POT",price:1.25,img:"https://image2url.com/r2/default/images/1769340321220-95e1be82-28fa-403a-a021-941d493283b8.png",stock:2,type:"egg"},
{name:"Axolotl Fly Ride",price:2,img:"https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png",stock:3,type:"pet"},
{name:"Cerberus Fly Ride",price:3,img:"https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg",stock:2,type:"pet"},
{name:"Dango Penguins",price:10,img:"https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png",stock:1,type:"pet"},
{name:"Neon Sneak Weasel (5)",price:12,img:"https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png",stock:2,type:"pet"},
{name:"Ride Sakura Spirit",price:8,img:"https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg",stock:1,type:"pet"},
{name:"Snow Owl Fly Ride",price:2.5,img:"https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg",stock:4,type:"pet"}
];
let cart=[];
const eggsDiv=document.getElementById('eggs');
const petsDiv=document.getElementById('pets');
const updatesUl=document.getElementById('updateList');
function render(){eggsDiv.innerHTML='';petsDiv.innerHTML='';items.forEach(i=>{
  const card=document.createElement('div');
  card.className='card';
  card.innerHTML=`<div class="card-img"><img src="${i.img}"></div><h3>${i.name}</h3><div class="price">$${i.price}</div><div class="stock">Stock: ${i.stock}</div><button ${i.stock===0?'disabled':''}>Add to Cart</button>`;
  card.querySelector('button').onclick=()=>addToCart(i);
  (i.type==='egg'?eggsDiv:petsDiv).appendChild(card);
})
}
function addToCart(item){cart.push(item);item.stock--;render();renderCart();playSound();}
function renderCart(){
  const c=document.getElementById('cartItems');
  c.innerHTML='';
  let total=0;
  cart.forEach((i,idx)=>{
    total+=i.price;
    const div=document.createElement('div');
    div.className='cart-item';
    div.innerHTML=`<img src="${i.img}"><span>${i.name}</span><span class="remove" onclick="removeCart(${idx})">✕</span>`;
    c.appendChild(div);
  });
  document.getElementById('total').innerText=`Total: $${total.toFixed(2)}`;
}
function removeCart(idx){cart.splice(idx,1);renderCart();render();}
document.getElementById('checkout').onclick=()=>{
  if(cart.length===0){alert('Cart empty');return;}
  let text='🛒 Oceanzx Order:\n';
  cart.forEach(i=>text+=`• ${i.name} - $${i.price}\n`);
  text+=`\n💰 Total: $${cart.reduce((a,b)=>a+b.price,0).toFixed(2)}`;
  navigator.clipboard.writeText(text);
  window.open('https://discord.gg/sv6tRJBR5G','_blank');
  cart=[];renderCart();render();
}
const audio=new Audio('https://freesound.org/data/previews/522/522998_10536942-lq.mp3');
function playSound(){audio.currentTime=0;audio.play();}
let viewers=27;
setInterval(()=>{viewers=Math.floor(Math.random()*50)+10;document.getElementById('viewing').innerText=`👀 ${viewers} people viewing`;},5000);
const devBtn=document.getElementById('devBtn');
devBtn.onclick=()=>{
  const pw=prompt('Enter password');
  if(pw==='Keebs'){
    const msg=prompt('Enter stock update text');
    if(msg) {
      const li=document.createElement('li');
      li.innerText=msg;
      updatesUl.appendChild(li);
      document.getElementById('updates').style.display='block';
    }
  }
}
render();
</script>
</body>
</html>
