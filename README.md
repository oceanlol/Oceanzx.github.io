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
    color:#e0e0e0;
    overflow-x:hidden;
}

/* Floating dots */
.dot {
    position:absolute;
    width:4px;
    height:4px;
    background:white;
    border-radius:50%;
    opacity:0.7;
    animation: float 15s linear infinite;
}
@keyframes float {
    from { transform: translateY(-10vh); }
    to { transform: translateY(120vh); }
}

header {
    text-align:center;
    padding:20px;
    background:#111;
    border-radius:0 0 20px 20px;
}

.container {
    max-width:1000px;
    margin:20px auto;
    padding:15px;
    background:#1a1a1a;
    border-radius:20px;
}

.grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
    gap:20px;
}

.item {
    background:#222;
    padding:15px;
    border-radius:18px;
    text-align:center;
    transition:0.3s;
}
.item:hover {
    transform:translateY(-5px);
    box-shadow:0 6px 15px rgba(255,255,255,0.15);
}

.item img {
    width:100%;
    max-width:140px;
    height:140px;
    object-fit:cover;
    border-radius:15px;
}

.price {
    color:#aaa;
    margin:5px 0;
}

.add-btn {
    background:#0a84ff;
    border:none;
    padding:8px 14px;
    border-radius:12px;
    color:white;
    font-weight:bold;
    cursor:pointer;
}
.add-btn:hover {
    background:#0066cc;
}

footer {
    text-align:center;
    padding:15px;
    color:#888;
}
</style>
</head>

<body>

<header>
    <h1>Oceanzx Adopt Me Shop</h1>
    <p>Fast delivery • Trusted trades • DM before payment</p>
</header>

<div class="container">
    <h2 style="text-align:center;">🔥 Available Pets 🔥</h2>

    <div class="grid">

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312696977-97a3b12d-0869-4661-86d5-65f8f181744a.png">
            <h3>Axolotl Fly Ride</h3>
            <div class="price">$2</div>
            <button class="add-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312266778-b30a7b97-61bb-4650-bc6c-45a73512c0ba.jpg">
            <h3>Cerberus Fly Ride</h3>
            <div class="price">$3</div>
            <button class="add-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312623274-1c54447a-0b15-4ac9-a9b6-c875cecd6076.png">
            <h3>Dango Penguins</h3>
            <div class="price">$10</div>
            <button class="add-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312555909-e343e380-5694-43a1-9ddf-df2b262990c4.png">
            <h3>Neon Sneak Weasel (5)</h3>
            <div class="price">$12</div>
            <button class="add-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312389581-e6410de1-5faa-4d25-8b23-dcf7c38fb51e.jpg">
            <h3>Ride Sakura Spirit</h3>
            <div class="price">$8</div>
            <button class="add-btn" onclick="buy()">Buy</button>
        </div>

        <div class="item">
            <img src="https://image2url.com/r2/default/images/1769312167327-6f2f8ab6-16e0-45d1-9730-dc8a16d6acdd.jpg">
            <h3>Snow Owl Fly Ride</h3>
            <div class="price">$2.50</div>
            <button class="add-btn" onclick="buy()">Buy</button>
        </div>

    </div>
</div>

<footer>
© 2026 Oceanzx Adopt Me Shop
</footer>

<script>
// floating dots
for(let i=0;i<80;i++){
    const d=document.createElement("div");
    d.className="dot";
    d.style.left=Math.random()*100+"vw";
    d.style.animationDuration=(8+Math.random()*12)+"s";
    document.body.appendChild(d);
}

// Buy button
function buy(){
    window.open("https://discord.com/users/1455058787257024512","_blank");
}
</script>

</body>
</html>
