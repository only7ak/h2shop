# h2shop[Uploadin<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>H2 Shop</title>
<style>
  :root {
    --purple-dark: #3a0ca3;
    --black-bg: #000000;
    --white: #ffffff;
    --gray-dark: #121212;
  }
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    background: var(--black-bg);
    color: var(--white);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    position: relative;
  }
  header {
    position: relative;
    background: var(--purple-dark);
    color: var(--white);
    padding: 20px;
    text-align: center;
    font-weight: bold;
    font-size: 2rem;
    box-shadow: 0 0 15px var(--purple-dark);
  }
  .logo {
    position: absolute;
    top: 10px;
    right: 10px;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    border: 2px solid var(--white);
    background: var(--purple-dark);
    object-fit: contain;
  }
  main {
    flex: 1;
    max-width: 900px;
    margin: 30px auto 50px auto;
    width: 90%;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    min-height: 400px;
  }
  .product-card {
    background: var(--gray-dark);
    border-radius: 12px;
    padding: 15px;
    box-shadow: 0 4px 15px rgba(58, 12, 163, 0.6);
    display: flex;
    flex-direction: column;
    color: var(--white);
    transition: transform 0.25s ease;
    width: 280px;
    cursor: pointer;
  }
  .product-card:hover {
    transform: translateY(-7px);
    box-shadow: 0 8px 30px var(--purple-dark);
  }
  .product-card img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 10px;
    margin-bottom: 12px;
    border: 2px solid var(--purple-dark);
    background: #000;
  }
  .product-name {
    font-size: 1.2rem;
    font-weight: 600;
    color: var(--purple-dark);
    margin-bottom: 8px;
  }
  .product-price {
    font-weight: bold;
    font-size: 1.1rem;
    margin-bottom: 12px;
    color: var(--white);
  }
  /* زر أضف إلى السلة داخل البطاقة لنستخدمها في popup */
  .btn {
    background-color: var(--purple-dark);
    color: var(--white);
    border: none;
    border-radius: 10px;
    padding: 10px 15px;
    font-weight: 700;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  .btn:hover {
    background-color: #270871;
  }

  /* صندوق السلة في أسفل يمين */
  #cart {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: var(--purple-dark);
    padding: 15px 25px;
    border-radius: 30px;
    box-shadow: 0 4px 15px rgba(58, 12, 163, 0.8);
    font-weight: bold;
    cursor: pointer;
    user-select: none;
    color: var(--white);
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 1.1rem;
  }
  #cart-icon {
    width: 24px;
    height: 24px;
    filter: invert(1);
  }

  /* نافذة البوب اب */
  #popup {
    display: none; /* مخفي بشكل افتراضي */
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: var(--gray-dark);
    padding: 25px;
    border-radius: 15px;
    box-shadow: 0 0 25px var(--purple-dark);
    max-width: 350px;
    width: 90%;
    z-index: 1000;
    color: var(--white);
  }
  #popup img {
    width: 100%;
    border-radius: 10px;
    margin-bottom: 15px;
    object-fit: cover;
    background: #000;
  }
  #popup .product-name {
    color: var(--purple-dark);
    font-size: 1.5rem;
    margin-bottom: 10px;
  }
  #popup .product-desc {
    font-size: 1rem;
    margin-bottom: 20px;
    line-height: 1.4;
  }
  #popup .btn-close {
    background: transparent;
    border: none;
    color: var(--white);
    font-size: 1.2rem;
    position: absolute;
    top: 10px;
    left: 15px;
    cursor: pointer;
  }

  /* خلفية شفافة خلف البوب اب */
  #overlay {
    display: none;
    position: fixed;
    top: 0; left: 0;
    width: 100vw; height: 100vh;
    background: rgba(0,0,0,0.7);
    z-index: 900;
  }
</style>
</head>
<body>
<header>
  H2 Shop
  <img
    src="https://cdn-icons-png.flaticon.com/512/880/880628.png"
    alt="شعار H2 Shop"
    class="logo"
  />
</header>
<main>
  <article class="product-card" id="product1">
    <img
      src="https://i.pinimg.com/originals/eb/1d/53/eb1d5393f24e8c1c25b5f426db0606a1.jpg"
      alt="حساب فورت نادر🤩"
    />
    <h2 class="product-name">حساب فورت نادر🤩</h2>
    <p class="product-price">٩ ﷼</p>
  </article>
</main>

<!-- سلة الشراء -->
<div id="cart" title="السلة">
  <img id="cart-icon" src="https://cdn-icons-png.flaticon.com/512/1170/1170678.png" alt="cart icon" />
  <span id="cart-count">0</span> منتج
</div>

<!-- نافذة البوب اب -->
<div id="overlay"></div>
<div id="popup">
  <button class="btn-close" title="إغلاق">×</button>
  <img
    src="https://i.pinimg.com/originals/eb/1d/53/eb1d5393f24e8c1c25b5f426db0606a1.jpg"
    alt="حساب فورت نادر🤩"
    id="popup-img"
  />
  <h2 class="product-name" id="popup-name">حساب فورت نادر🤩</h2>
  <p class="product-desc" id="popup-desc">
    حساب فورت نايت نادر جداً مع مجموعة من الأسلحة والجلود الحصرية. مثالي لمحبي اللعبة الذين يريدون التميز.
  </p>
  <p class="product-price" id="popup-price">٩ ﷼</p>
  <button class="btn" id="add-to-cart-btn">أضف إلى السلة</button>
</div>

<script>
  const productCard = document.getElementById('product1');
  const popup = document.getElementById('popup');
  const overlay = document.getElementById('overlay');
  const btnClose = popup.querySelector('.btn-close');
  const cart = document.getElementById('cart');
  const cartCount = document.getElementById('cart-count');
  const addToCartBtn = document.getElementById('add-to-cart-btn');

  let cartItems = 0;

  productCard.addEventListener('click', () => {
    popup.style.display = 'block';
    overlay.style.display = 'block';
  });

  btnClose.addEventListener('click', closePopup);
  overlay.addEventListener('click', closePopup);

  function closePopup() {
    popup.style.display = 'none';
    overlay.style.display = 'none';
  }

  addToCartBtn.addEventListener('click', () => {
    cartItems++;
    cartCount.textContent = cartItems;
    alert('تم إضافة حساب فورت نادر🤩 إلى السلة!');
    closePopup();
  });

  cart.addEventListener('click', () => {
    alert(`السلة تحتوي على ${cartItems} منتج(منتجات).`);
  });
</script>
</body>
</html>g H2shop.html…]()
