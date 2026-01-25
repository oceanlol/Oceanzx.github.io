<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Adopt Me Shop</title>

<style>
:root{
    --accent:#0a84ff;
    --card:#1f1f1f;
    --soft:#2a2a2a;
}

*{box-sizing:border-box}

body{
    margin:0;
    font-family: "Segoe UI", Arial, sans-serif;
    background:black;
    color:#f2f2f2;
    overflow-x:hidden;
}

/* floating dots */
.dot{
    position:absolute;
    width:3px;
    height:3px;
    background:white;
    border-radius:50%;
    opacity:0.6;
    animation: float linear infinite;
}
@keyframes float{
    from{transform:translateY(-10vh)}
    to{transform:translateY(120vh)}
}

/* header */
header{
    text-align:center;
    padding:30px 20px;
    background:linear-gradient(180deg,#111,#000);
    border-bottom:1px solid #333;
}
header h1{
    margin:0;
    font-size:2rem;
    letter-spacing:1px;
}
header p{
    margin-top:8px;
    font-size:0.9rem;
    color:#aaa;
}

/* main container */
.container{
    max-width:1100px;
    margin:30px auto;
    padding:20px;
    background:rgba(20,20,20,0.9);
    border-radius:28px;
    box-shadow:0 0 40px rgba(10,132,255,0.08);
}

.section-title{
    text-align:center;
    font-size:1.6rem;
    margin-bottom:25px;
}

/* grid */
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:25px;
}

/* product card */
.item{
    background:linear-gradient(180deg,var(--card),#151515);
    padding:18px;
    border-radius:26px;
    text-align:center;
    transition:0.35s;
    position:relative;
}
.item::after{
    content:"";
    position:absolute;
    inset:0;
    border-radius:26px;
    box-shadow:0 0 0 rgba(10,132,255,0);
    transition:0.35s;
}
.item:hover{
    transform:translateY(-6px) scale(1.01);
}
.item:hover::after{
    box-shadow:0 0 25px rgba(10,132,255,0.35);
}

.item img{
    width:100%;
    max-width:150px;
    height:150px;
    object-fit:cover;
    border-radius:22px;
    margin-bottom:12px;
}

.item h3{
    margin:8px 0 4px;
    font-size:1rem;
}

.price{
    color:#bdbdbd;
    font-weight:bold;
    margin-bottom:12px;
}

/* buy button */
.buy-btn{
    background:linear-gradient(180deg,var(--accent),#0066cc);
    border:none;
    padding:10px 18px;
    border-radius:18px;
    color:white;
    font-weight:bold;
    cursor:pointer;
    transition:0.3s;
}
.buy-btn:hover{
    transform:scale(1.06);
    filter:brightness(1.15);
}

/* footer */
footer{
    text-align:center;
    padding:20px;
    color:#777;
    font-size:0.85rem;
}

/* mobile tweaks */
@media(max-width:480px){
    header h1{font-size:1.6rem}
    .container{margin:15px}
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

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png">
            <h3>Axolotl Fly Ride</h3>
            <div class="price">$2</div>
            <button class="buy-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg">
            <h3>Cerberus Fly Ride</h3>
            <div class="price">$3</div>
            <button class="buy-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png">
            <h3>Dango Penguins</h3>
            <div class="price">$10</div>
            <button class="buy-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png">
            <h3>Neon Sneak Weasel (5)</h3>
            <div class="price">$12</div>
            <button class="buy-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg">
            <h3>Ride Sakura Spirit</h3>
            <div class="price">$8</div>
            <button class="buy-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg">
            <h3>Snow Owl Fly Ride</h3>
            <div class="price">$2.50</div>
            <button class="buy-btn" onclick="buy()">Buy</button>
        </div>

    </div>
</div>

<footer>
© 2026 Oceanzx Adopt Me Shop
</footer>

<script>
for(let i=0;i<90;i++){
    const d=document.createElement("div");
    d.className="dot";
    d.style.left=Math.random()*100+"vw";
    d.style.animationDuration=(10+Math.random()*15)+"s";
    document.body.appendChild(d);
}

function buy(){
    window.open("https://discord.com/users/1455058787257024512","_blank");
}
</script>

</body>
</html>
