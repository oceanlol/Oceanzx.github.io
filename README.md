<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Shop</title>
<style>
body{
    background:black;
    color:white;
    font-family:Arial;
    text-align:center;
    padding:60px 20px;
}
button{
    padding:16px 32px;
    margin:20px;
    font-size:1.2rem;
    border-radius:20px;
    border:none;
    background:#0a84ff;
    color:white;
    cursor:pointer;
}
button:hover{background:#0066cc}
</style>
</head>
<body>

<h1>Welcome to Oceanzx Adopt Me Shop</h1>
<p>Choose your device</p>

<button onclick="goPhone()">📱 Phone</button>
<button onclick="goDesktop()">💻 Desktop</button>

<script>
function goPhone(){location.href="mobile/index.html";}
function goDesktop(){location.href="desktop/index.html";}

// auto-detect
if(/Mobi|Android|iPhone/i.test(navigator.userAgent)){
    goPhone();
}
</script>

</body>
</html>
