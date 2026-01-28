
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OCEANZX</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,Helvetica,sans-serif;
  background:#000;
  color:#fff;
  overflow-x:hidden;
}

/* PARTICLES */
canvas{
  position:fixed;
  top:0;
  left:0;
  width:100%;
  height:100%;
  z-index:-1;
}

/* LAYOUT */
header{
  text-align:center;
  padding:60px 20px 30px;
}
header h1{
  letter-spacing:6px;
  font-weight:700;
  margin:0;
}
header p{
  color:#aaa;
  margin-top:10px;
  font-size:14px;
}

.container{
  max-width:1200px;
  margin:auto;
  padding:20px;
}

.section-title{
  font-size:22px;
  letter-spacing:2px;
  margin:60px 0 20px;
  border-bottom:1px solid #222;
  padding-bottom:10px;
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(220px,1fr));
  gap:28px;
}

.card{
  background:#0a0a0a;
  border:1px solid #1a1a1a;
  border-radius:18px;
  padding:16px;
  text-align:center;
  transition:.25s;
}
.card:hover{
  transform:translateY(-6px);
  border-color:#fff;
}
.card img{
  width:100%;
  height:180px;
  object-fit:contain;
  filter:grayscale(100%) contrast(1.1);
}
.card h3{
  font-size:15px;
  margin:14px 0 4px;
}
.price{
  font-weight:bold;
  font-size:14px;
}
.stock{
  font-size:12px;
  color:#aaa;
  margin-top:6px;
}
.btn{
  margin-top:12px;
  width:100%;
  padding:10px;
  background:#fff;
  color:#000;
  border:none;
  border-radius:14px;
  font-weight:bold;
  cursor:pointer;
}
.btn:hover{opacity:.85}
.btn:disabled{
  background:#444;
  color:#888;
  cursor:not-allowed;
}

/* CART */
#cart{
  position:fixed;
  right:20px;
  top:20px;
  width:300px;
  background:#0a0a0a;
  border:1px solid #1f1f1f;
  border-radius:18px;
  padding:16px;
}
#cart h3{margin-top:0}
#cart-items{
  max-height:260px;
  overflow-y:auto;
  font-size:13px;
}
.cart-item{
  display:flex;
  justify-content:space-between;
  margin:6px 0;
}
.total{
  margin-top:10px;
  font-weight:bold;
}
.checkout{
  margin-top:10px;
}

/* SCROLLBAR */
#cart-items::-webkit-scrollbar{width:6px}
#cart-items::-webkit-scrollbar-thumb{background:#333;border-radius:10px}
</style>
</head>

<body>

<canvas id="particles"></canvas>

<header>
  <h1>OCEANZX</h1>
  <p>Adopt Me Store • Cash App Only</p>
</header>

<div class="container">

  <!-- PETS FIRST -->
  <div class="section-title">PETS</div>
  <div class="grid" id="pets"></div>

  <!-- EGGS SECOND -->
  <div class="section-title">EGGS</div>
  <div class="grid" id="eggs"></div>

</div>

<div id="cart">
  <h3>CART</h3>
  <div id="cart-items"></div>
  <div class="total">Total: $<span id="total">0.00</span></div>
  <button class="btn checkout" onclick="checkout()">Checkout</button>
</div>

<script>
// ===== PARTICLES =====
const canvas=document.getElementById("particles");
const ctx=canvas.getContext("2d");
let w,h;
function resize(){w=canvas.width=window.innerWidth;h=canvas.height=window.innerHeight}
window.onresize=resize;resize();

let dots=[...Array(120)].map(()=>({
  x:Math.random()*w,
  y:Math.random()*h,
  vx:(Math.random()-.5)*1.5,
  vy:(Math.random()-.5)*1.5
}));

function animate(){
  ctx.clearRect(0,0,w,h);
  ctx.fillStyle="#fff";
  dots.forEach(d=>{
    d.x+=d.vx; d.y+=d.vy;
    if(d.x<0||d.x>w) d.vx*=-1;
    if(d.y<0||d.y>h) d.vy*=-1;
    ctx.beginPath();
    ctx.arc(d.x,d.y,1.3,0,Math.PI*2);
    ctx.fill();
  });
  requestAnimationFrame(animate);
}
animate();

// ===== STORE DATA =====
const pets=[
 {n:"Strawberry Bat Dragon FR",p:24,s:5,i:"https://image2url.com/r2/default/images/1769419915326-9b1f86be-1cf1-47e3-9eac-43f7fb10c8ba.png"},
 {n:"Cow Fly Ride",p:20,s:5,i:"https://image2url.com/r2/default/images/1769419943380-9a948b0d-6c67-40d8-960b-79564c520a19.png"},
 {n:"Turtle Fly Ride",p:22.1,s:5,i:"https://image2url.com/r2/default/images/1769417980360-be5c9242-f50d-4c26-8b02-38ad8b169e91.png"},
 {n:"Unicorn",p:3.25,s:5,i:"https://image2url.com/r2/default/images/1769417779444-cc940dbb-8d7e-4e91-8e22-998da1983d02.png"}
];

const eggs=[
 {n:"Crystal Egg",p:1,s:15,i:"https://image2url.com/r2/default/images/1769419308180-be119059-935c-4323-8d8a-2d0e5958128c.png"},
 {n:"Retired Egg",p:.5,s:15,i:"https://image2url.com/r2/default/images/1769419815185-0d947ffd-f776-439d-9ae8-369f4da2547f.png"},
 {n:"Moon Egg",p:.63,s:15,i:"https://image2url.com/r2/default/images/1769419776495-b06541d7-00ea-4c74-856a-a6ce4d29b8b6.png"},
 {n:"Royal Egg",p:.2,s:15,i:"https://image2url.com/r2/default/images/1769419849095-5a4e63b2-ad03-4efa-98bd-54607cbec21d.png"}
];

let cart=[];

// ===== RENDER =====
function render(list,el){
  el.innerHTML="";
  list.forEach((x,i)=>{
    el.innerHTML+=`
    <div class="card">
      <img src="${x.i}">
      <h3>${x.n}</h3>
      <div class="price">$${x.p}</div>
      <div class="stock">Stock: ${x.s}</div>
      <button class="btn" ${x.s<=0?"disabled":""} onclick="add(${list===pets?'pets':'eggs'},${i})">
        ${x.s<=0?"Sold Out":"Add"}
      </button>
    </div>`;
  });
}

function add(arr,i){
  if(arr[i].s<=0)return;
  arr[i].s--;
  cart.push(arr[i]);
  update();
}

function update(){
  render(pets,document.getElementById("pets"));
  render(eggs,document.getElementById("eggs"));
  let t=0;
  const c=document.getElementById("cart-items");
  c.innerHTML="";
  cart.forEach(i=>{t+=i.p;c.innerHTML+=`<div class="cart-item"><span>${i.n}</span><span>$${i.p}</span></div>`});
  document.getElementById("total").innerText=t.toFixed(2);
}

function checkout(){
  let text="OCEANZX ORDER\n\n";
  let t=0;
  cart.forEach(i=>{text+=`• ${i.n} - $${i.p}\n`;t+=i.p});
  text+=`\nTotal: $${t}\nCashApp ONLY: $Bananaboy723`;
  navigator.clipboard.writeText(text);
  window.open("https://discord.gg/sv6tRJBR5G","_blank");
  cart=[];
  update();
}

update();
</script>

</body>
</html>
