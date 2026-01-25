<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>
<style>
/* General */
body {
  margin:0;
  font-family: Arial, sans-serif;
  background: black;
  color: #e0e0e0;
  overflow-x: hidden;
}

.dot {
  position: absolute;
  border-radius: 50%;
  background: white;
  opacity: 0.8;
  animation: moveDot linear infinite;
}
@keyframes moveDot {
  0% { transform: translateY(0) translateX(0); }
  100% { transform: translateY(120vh) translateX(50vw); }
}

/* Header */
header {
  text-align:center;
  padding:20px;
  background:#111;
  border-bottom:2px solid #444;
  border-radius:0 0 20px 20px;
}
header h1 { margin:0; font-size:1.6rem; }
header p { margin:5px 0 0; font-size:0.9rem; color:#ccc; }

/* Container & Grid */
.container { max-width:1000px; margin:20px auto; padding:15px; background:#1a1a1a; border-radius:20px; }
.section-title { text-align:center; font-size:1.4rem; margin:20px 0; }
.grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(160px,1fr)); gap:20px; justify-items:center; }

.item {
  background:#222;
  padding:15px;
  border-radius:15px;
  display:flex;
  flex-direction:column;
  align-items:center;
  transition: transform 0.3s, box-shadow 0.3s;
}
.item:hover { transform:translateY(-3px); box-shadow:0 5px 12px rgba(255,255,255,0.2); }

.product-img { width:100%; max-width:140px; height:140px; object-fit:cover; border-radius:15px; margin-bottom:10px; }
.item-name { font-weight:bold; font-size:0.95rem; text-align:center; margin-bottom:5px; }
.item-price { color:#aaa; font-weight:bold; margin-bottom:10px; }

.add-btn {
  background:#333; color:#fff; border:none; padding:8px 14px; border-radius:12px; cursor:pointer; font-weight:bold; font-size:0.85rem; transition:all 0.3s;
}
.add-btn:hover { background:#555; transform:scale(1.05); }

/* Cart */
#cart {
  position: fixed; top:20px; right:20px; background:#111; border:2px solid #444; border-radius:15px; padding:15px; width:260px; max-height:70vh; overflow-y:auto; z-index:10;
}
#cart h3 { margin-top:0; margin-bottom:10px; font-size:1rem; text-align:center; position:relative; }
#cart-count {
  position:absolute; top:-10px; right:-10px; background:#0a84ff; color:#fff; border-radius:50%; width:22px; height:22px; display:flex; justify-content:center; align-items:center; font-size:0.75rem; font-weight:bold;
}
.cart-item { display:flex; justify-content:space-between; align-items:center; margin-bottom:8px; font-size:0.85rem; }
.cart-item img { margin-right:8px; border-radius:5px; width:35px; height:35px; object-fit:cover; }
.cart-total { font-weight:bold; margin-top:8px; text-align:right; }
.checkout-btn { background:#0a84ff; color:#fff; width:100%; border:none; padding:8px; border-radius:12px; font-weight:bold; cursor:pointer; margin-top:10px; transition:0.3s; }
.checkout-btn:hover { background:#0066cc; }

/* Fullscreen Overlay for Screenshot */
#checkout-overlay {
  display:none; position:fixed; top:0; left:0; width:100vw; height:100vh; background: rgba(0,0,0,0.95); color:#fff; z-index:1000; padding:50px 20px; text-align:center; overflow-y:auto; opacity:0; transform:translateY(-50px); transition: opacity 0.5s ease, transform 0.5s ease;
}
#checkout-overlay.active { display:block; opacity:1; transform:translateY(0); }

#checkout-overlay h2 { font-size:1.8rem; margin-bottom:20px; }
#checkout-overlay p { font-size:1rem; margin-bottom:20px; }
#checkout-overlay .overlay-cart { text-align:left; max-width:500px; margin:0 auto; background:#222; padding:20px; border-radius:15px; }
#checkout-overlay .overlay-cart .cart-item { display:flex; align-items:center; margin-bottom:8px; }
#overlay-close, #copy-total-btn { background:#0a84ff; color:#fff; border:none; padding:10px 20px; border-radius:12px; font-weight:bold; cursor:pointer; margin-top:20px; transition:0.3s; display:block; margin-left:auto; margin-right:auto; }
#overlay-close:hover, #copy-total-btn:hover { background:#0066cc; }

/* Footer */
footer { text-align:center; padding:12px; margin-top:30px; color:#aaa; font-size:0.85rem; }

/* Mobile tweaks */
@media(max-width:480px){
  .grid { gap:15px; }
  .product-img { max-width:120px; height:120px; }
  #cart { width:200px; padding:10px; top:10px; right:10px; }
  .checkout-btn, #overlay-close, #copy-total-btn { padding:6px; font-size:0.8rem; }
  #checkout-overlay { padding:20px 10px; }
}
</style>
</head>
<body>

<header>
  <h1>Oceanzx Adopt Me Shop</h1>
  <p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="container">
  <div class="section-title">🔥 Available Pets 🔥</div>
  <div class="grid">
    <div class="item" data-name="Axolotl Fly Ride" data-price="2">
      <img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png" class="product-img">
      <div class="item-name">Axolotl Fly Ride</div>
      <div class="item-price">$2</div>
      <button class="add-btn">Add to Cart</button>
    </div>
    <div class="item" data-name="Cerberus Fly Ride" data-price="3">
      <img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg" class="product-img">
      <div class="item-name">Cerberus Fly Ride</div>
      <div class="item-price">$3</div>
      <button class="add-btn">Add to Cart</button>
    </div>
    <div class="item" data-name="Dango Penguins" data-price="10">
      <img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png" class="product-img">
      <div class="item-name">Dango Penguins</div>
      <div class="item-price">$10</div>
      <button class="add-btn">Add to Cart</button>
    </div>
    <div class="item" data-name="Neon Sneak Weasel (5)" data-price="12">
      <img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png" class="product-img">
      <div class="item-name">Neon Sneak Weasel (5)</div>
      <div class="item-price">$12</div>
      <button class="add-btn">Add to Cart</button>
    </div>
    <div class="item" data-name="Ride Sakura Spirit" data-price="8">
      <img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg" class="product-img">
      <div class="item-name">Ride Sakura Spirit</div>
      <div class="item-price">$8</div>
      <button class="add-btn">Add to Cart</button>
    </div>
    <div class="item" data-name="Snow Owl Fly Ride" data-price="2.5">
      <img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg" class="product-img">
      <div class="item-name">Snow Owl Fly Ride</div>
      <div class="item-price">$2.50</div>
      <button class="add-btn">Add to Cart</button>
    </div>
  </div>
</div>

<!-- Cart -->
<div id="cart">
  <h3>Cart <span id="cart-count">0</span></h3>
  <div id="cart-items"></div>
  <div class="cart-total" id="cart-total">Total: $0.00</div>
  <button class="checkout-btn" id="checkout">Checkout</button>
</div>

<!-- Checkout Overlay -->
<div id="checkout-overlay">
  <h2>Take a Screenshot of Your Cart</h2>
  <p>Make sure your cart is fully visible. Then click "Copy Total & Go to Discord".</p>
  <div class="overlay-cart" id="overlay-cart"></div>
  <button id="copy-total-btn">Copy Total to Clipboard 💰</button>
  <button id="overlay-close">Confirm & Go to Discord</button>
</div>

<footer>
  &copy; 2026 Oceanzx Adopt Me Shop
</footer>

<script>
// Background dots
const numDots = 100;
for(let i=0;i<numDots;i++){
  const dot=document.createElement('div'); dot.classList.add('dot');
  const size=Math.random()*3+1; dot.style.width=dot.style.height=size+'px';
  dot.style.top=Math.random()*window.innerHeight+'px'; dot.style.left=Math.random()*window.innerWidth+'px';
  dot.style.animationDuration=(20+Math.random()*40)+'s';
  document.body.appendChild(dot);
}

// Cart logic
let cart = [];
const cartItemsDiv = document.getElementById('cart-items');
const cartTotalDiv = document.getElementById('cart-total');
const cartCount = document.getElementById('cart-count');
const overlay = document.getElementById('checkout-overlay');
const overlayCart = document.getElementById('overlay-cart');

function renderCart() {
  cartItemsDiv.innerHTML = '';
  overlayCart.innerHTML = '';
  let total=0;

  cart.forEach((item,index)=>{
    total += item.price;

    // Sidebar
    const div = document.createElement('div'); div.className='cart-item';
    div.style.display='flex'; div.style.alignItems='center'; div.style.justifyContent='space-between';

    const left = document.createElement('div'); left.style.display='flex'; left.style.alignItems='center';
    const thumb = document.createElement('img'); thumb.src=item.img;
    thumb.style.width='35px'; thumb.style.height='35px'; thumb.style.marginRight='10px'; thumb.style.borderRadius='5px'; thumb.style.objectFit='cover';
    const text = document.createElement('span'); text.textContent=`${item.name} - $${item.price.toFixed(2)}`;
    left.appendChild(thumb); left.appendChild(text);

    const removeBtn=document.createElement('button'); removeBtn.textContent='Remove'; removeBtn.style.cursor='pointer';
    removeBtn.onclick=()=>{ cart.splice(index,1); renderCart(); }

    div.appendChild(left); div.appendChild(removeBtn);
    cartItemsDiv.appendChild(div);

    // Overlay
    const overlayDiv=document.createElement('div'); overlayDiv.className='cart-item'; overlayDiv.style.display='flex'; overlayDiv.style.alignItems='center'; overlayDiv.style.marginBottom='8px';
    const overlayThumb=document.createElement('img'); overlayThumb.src=item.img; overlayThumb.style.width='40px'; overlayThumb.style.height='40px'; overlayThumb.style.marginRight='10px'; overlayThumb.style.borderRadius='8px'; overlayThumb.style.objectFit='cover';
    const overlayText=document.createElement('span'); overlayText.textContent=`${item.name} - $${item.price.toFixed(2)}`;
    overlayDiv.appendChild(overlayThumb); overlayDiv.appendChild(overlayText);
    overlayCart.appendChild(overlayDiv);
  });

  cartTotalDiv.textContent="Total: $"+total.toFixed(2);
  cartCount.textContent=cart.length;
}

// Add to cart buttons
document.querySelectorAll('.add-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    const itemDiv=btn.closest('.item');
    const name=itemDiv.dataset.name;
    const price=parseFloat(itemDiv.dataset.price);
    const img=itemDiv.querySelector('img').src;
    cart.push({name,price,img});
    renderCart();
  });
});

// Checkout
document.getElementById('checkout').addEventListener('click',()=>{
  if(cart.length===0){ alert("Your cart is empty!"); return; }
  overlay.classList.add('active');
});

// Copy total for Cash App
document.getElementById('copy-total-btn').addEventListener('click',()=>{
  const total = cart.reduce((sum,item)=>sum+item.price,0).toFixed(2);
  navigator.clipboard.writeText(total).then(()=>{ alert(`Total $${total} copied! Paste this in Cash App to pay.`); });
});

// Go to Discord
document.getElementById('overlay-close').addEventListener('click',()=>{
  if(cart.length===0){ overlay.classList.remove('active'); return; }
  window.open('https://discord.gg/sv6tRJBR5G','_blank');
  overlay.classList.remove('active'); 
});
</script>

</body>
</html>
