<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Oceanzx Shop - Choose Device</title>
<style>
body {background:black;color:white;font-family:Arial;text-align:center;padding:50px;}
button {padding:15px 30px;margin:20px;font-size:1.2rem;border-radius:15px;background:#333;color:#fff;border:none;cursor:pointer;transition:0.3s;}
button:hover {background:#555;transform:scale(1.05);}
h1{margin-bottom:30px;}
</style>
</head>
<body>

<h1>Welcome to Oceanzx Adopt Me Shop</h1>
<p>Which version do you want to view?</p>
<button onclick="goPhone()">📱 Phone Version</button>
<button onclick="goDesktop()">💻 Desktop Version</button>

<script>
function goPhone() {
    window.location.href = "mobile/index.html";
}
function goDesktop() {
    window.location.href = "desktop/index.html";
}

// Optional auto-detect phone
if (/Mobi|Android|iPhone/i.test(navigator.userAgent)) {
    // window.location.href = "mobile/index.html";
}
</script>

</body>
</html>
