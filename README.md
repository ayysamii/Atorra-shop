<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Arorra Shop</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 20px; background: #fffaf0; color: #333;
  }
  h1 {
    text-align: center; margin-bottom: 20px; color: #a52a2a;
  }
  .product-list {
    max-width: 700px; margin: auto;
  }
  .product {
    display: flex; justify-content: space-between; align-items: center;
    padding: 10px; background: #fff; margin-bottom: 10px; border-radius: 5px;
    box-shadow: 0 0 5px rgba(0,0,0,0.1);
  }
  .product-info {
    flex: 1;
  }
  button {
    background-color: #a52a2a; border: none; color: white;
    padding: 8px 15px; border-radius: 5px;
    cursor: pointer; font-weight: bold;
  }
  button:hover {
    background-color: #8b1a1a;
  }
  #cart {
    max-width: 700px; margin: 20px auto;
    padding: 15px; background: #fff0f0; border-radius: 7px;
    box-shadow: 0 0 8px rgba(165,42,42,0.3);
  }
  #cart h2 {
    margin-top: 0; color: #a52a2a;
  }
  #order-btn {
    background-color: #228b22; margin-top: 15px;
    width: 100%; font-size: 16px;
  }
</style>
</head>
<body>
<h1>متجر Arorra Shop</h1>

<div class="product-list" id="product-list">
  <!-- المنتجات -->
</div>

<div id="cart" style="display:none;">
  <h2>عربة التسوق</h2>
  <ul id="cart-items"></ul>
  <p><strong>الإجمالي: </strong><span id="total-price">0</span> LYD</p>
  <button id="order-btn">اطلب الآن عبر واتساب</button>
</div>

<script>
const products = [
  {name:"Dior face palette", price:290},
  {name:"Rosa glow blush", price:205},
  {name:"Lipstick Dior", price:195},
  {name:"Lip Glass maximiser", price:195},
  {name:"Dior eyeshadow palette", price:290},
  {name:"Dior lip oil", price:195},
  {name:"Dior iconic mascara", price:195},
  {name:"Dior handcream", price:200},
  {name:"Dior make-up pouch", price:0},
  {name:"Dior glow foundation", price:350},
  {name:"Dior full cover concealer", price:250}
];

const productListEl = document.getElementById("product-list");
const cartEl = document.getElementById("cart");
const cartItemsEl = document.getElementById("cart-items");
const totalPriceEl = document.getElementById("total-price");
const orderBtn = document.getElementById("order-btn");
const phoneNumber = "219123456789"; // عدلي هنا رقم الواتساب بالصيغة الدولية بدون + (مثلاً 219123456789)

let cart = [];

function renderProducts() {
  products.forEach((p, i) => {
    const div = document.createElement("div");
    div.className = "product";
    div.innerHTML = `
      <div class="product-info">
        <strong>${p.name}</strong> - ${p.price} LYD
      </div>
      <button onclick="addToCart(${i})">أضف للسلة</button>
    `;
    productListEl.appendChild(div);
  });
}

function addToCart(index) {
  const product = products[index];
  cart.push(product);
  renderCart();
}

function renderCart() {
  if(cart.length === 0) {
    cartEl.style.display = "none";
    return;
  }
  cartEl.style.display = "block";
  cartItemsEl.innerHTML = "";
  let total = 0;
  cart.forEach((item, idx) => {
    total += item.price;
    const li = document.createElement("li");
    li.textContent = `${item.name} - ${item.price} LYD`;
    cartItemsEl.appendChild(li);
  });
  totalPriceEl.textContent = total;
}

orderBtn.onclick = () => {
  if(cart.length === 0) {
    alert("السلة فارغة!");
    return;
  }
  let message = "طلب من Arorra Shop:%0A";
  cart.forEach(item => {
    message += `- ${item.name} : ${item.price} LYD%0A`;
  });
  message += `الإجمالي: ${totalPriceEl.textContent} LYD`;
  const url = `https://wa.me/${phoneNumber}?text=${message}`;
  window.open(url, "_blank");
}

renderProducts();
</script>
</body>
</html>
