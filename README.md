<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Scan 2 Dine</title>

<style>
body {
    font-family: Arial;
    text-align: center;
    background: #f4f4f4;
}

.container {
    margin-top: 20px;
}

.logo {
    font-size: 60px;
}

h1 {
    color: #333;
}

button {
    padding: 10px 20px;
    margin: 10px;
    background: orange;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.section {
    display: none;
}

.item {
    background: white;
    margin: 10px auto;
    padding: 10px;
    width: 200px;
    border-radius: 5px;
}
</style>
</head>

<body>

<div class="container">

    <!-- HOME -->
    <div id="home">
        <div class="logo">🍽️</div>
        <h1>Scan 2 Dine</h1>
        <p>Scan QR Code to Order Food</p>

        <img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=menu">

        <br><br>
        <button onclick="showMenu()">Scan QR</button>
    </div>

    <!-- MENU -->
    <div id="menu" class="section">
        <h2>Menu Card</h2>

        <div class="item">
            Pizza - ₹200
            <button onclick="addToCart('Pizza')">Add</button>
        </div>

        <div class="item">
            Burger - ₹150
            <button onclick="addToCart('Burger')">Add</button>
        </div>

        <div class="item">
            Pasta - ₹180
            <button onclick="addToCart('Pasta')">Add</button>
        </div>

        <button onclick="goToCart()">Go to Cart</button>
    </div>

    <!-- CART -->
    <div id="cart" class="section">
        <h2>Your Cart</h2>
        <ul id="cartItems"></ul>

        <label>Select Table Number:</label><br>
        <select id="table">
            <option>Table 1</option>
            <option>Table 2</option>
            <option>Table 3</option>
            <option>Table 4</option>
        </select>

        <br><br>
        <button onclick="goToPayment()">Proceed to Payment</button>
    </div>

    <!-- PAYMENT -->
    <div id="payment" class="section">
        <h2>Select Payment Method</h2>

        <label><input type="radio" name="pay"> UPI</label><br>
        <label><input type="radio" name="pay"> Card</label><br>
        <label><input type="radio" name="pay"> Cash</label><br>

        <br>
        <button onclick="placeOrder()">Pay Now</button>
    </div>

    <!-- SUCCESS -->
    <div id="success" class="section">
        <h2>✅ Order Placed Successfully!</h2>
        <p>Your Token Number: <strong id="token"></strong></p>
        <p>Food will be served shortly 🍽️</p>
    </div>

</div>

<script>
let cart = [];

function showMenu() {
    document.getElementById("home").style.display = "none";
    document.getElementById("menu").style.display = "block";
}

function addToCart(item) {
    cart.push(item);
    alert(item + " added to cart");
}

function goToCart() {
    document.getElementById("menu").style.display = "none";
    document.getElementById("cart").style.display = "block";

    let list = document.getElementById("cartItems");
    list.innerHTML = "";

    cart.forEach(item => {
        let li = document.createElement("li");
        li.textContent = item;
        list.appendChild(li);
    });
}

function goToPayment() {
    document.getElementById("cart").style.display = "none";
    document.getElementById("payment").style.display = "block";
}

function placeOrder() {
    document.getElementById("payment").style.display = "none";
    document.getElementById("success").style.display = "block";

    // Generate token number
    let token = Math.floor(1000 + Math.random() * 9000);
    document.getElementById("token").textContent = token;
}
</script>

</body>
</html>
<script>
fetch("https://order-handler-1--sahithiaddanki.replit.app")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.log(error);
  });
</script>
