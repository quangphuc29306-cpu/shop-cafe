# BÁO CÁO MÃ NGUỒN WEBSITE BÁN CÀ PHÊ - KVONE COFFEE

**Ngày lập báo cáo:** 25/12/2024  
**Người thực hiện:** Phân tích kỹ thuật Website

---

## TỔNG QUAN CÔNG NGHỆ

### Tên công nghệ (Framework, thư viện)

- **Front-end Framework:** Không sử dụng (Pure Vanilla JavaScript)
- **HTML:** HTML5
- **CSS:** CSS3 với kiến trúc Modular
- **JavaScript:** ES6+ (Vanilla JavaScript, không dùng thư viện như React, Vue, Angular)
- **Font chữ:** Google Fonts (Nunito, Playfair Display)
- **Icons:** Emoji Unicode (không dùng Font Awesome hay icon library khác)

### Công nghệ CSS nổi bật

- **CSS Variables (Custom Properties):** Quản lý màu sắc và spacing
- **CSS Grid & Flexbox:** Layout responsive
- **CSS Animations & Keyframes:** Hiệu ứng chuyển động
- **Glassmorphism:** `backdrop-filter: blur()`
- **3D Transforms:** `transform-style: preserve-3d`

### Công nghệ JavaScript nổi bật

- **Event Delegation with Capture Phase:** Tối ưu hiệu suất
- **LocalStorage API:** Lưu trữ dữ liệu client-side
- **Custom Events:** Giao tiếp giữa các modules
- **IIFE Pattern:** Đóng gói code, tránh pollution global scope
- **DocumentFragment:** Tối ưu DOM manipulation

### Đường dẫn hình ảnh

- **Tất cả đường dẫn:** Relative paths (ví dụ: `menu/banner.png`, `menu/icons/coffee.png`)
- **Không sử dụng:** External URLs hoặc CDN cho ảnh

---

## A. TRANG CHỦ (index.html)

### 1. Bố cục chính

#### a. Code HTML

```html
<!DOCTYPE html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Kvone Coffee - Thưởng thức cà phê chất lượng</title>
    <link rel="icon" type="image/png" href="menu/icons/coffee.png" />
    <link rel="stylesheet" href="css/main.css" />
  </head>
  <body>
    <div class="page-wrapper">
      <!-- Header -->
      <header class="header">...</header>

      <!-- Main Content -->
      <main class="main-content">
        <!-- Hero Section (Banner) -->
        <section class="hero">...</section>

        <!-- Products Section -->
        <section class="section" id="products">...</section>

        <!-- Features Section -->
        <section class="section">...</section>
      </main>

      <!-- Footer -->
      <footer class="footer">...</footer>
    </div>

    <!-- JavaScript Files -->
    <script src="js/storage.js"></script>
    <script src="js/auth.js"></script>
    <!-- ... các file JS khác ... -->
  </body>
</html>
```

**Giải thích:**

- `page-wrapper`: Container chính, sử dụng Flexbox để footer luôn ở cuối
- `main-content`: Nội dung chính, chiếm phần còn lại của viewport
- Không có inline styles, tất cả CSS được tách riêng

#### b. Code CSS định dạng chung

```css
/* File: css/base.css */

/* CSS Variables - Hệ thống màu sắc */
:root {
  --color-primary: #54372b; /* Nâu cà phê */
  --color-secondary: #f7e1bc; /* Màu kem */
  --color-background: #fff8ee; /* Nền sáng */
  --font-primary: "Nunito", sans-serif;
  --font-display: "Playfair Display", serif;
  --space-4: 1rem;
  --radius-xl: 1rem;
  --transition-normal: 300ms cubic-bezier(0.4, 0, 0.2, 1);
}

/* Reset CSS */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: var(--font-primary);
  background-color: var(--color-background);
  color: var(--color-text);
  line-height: 1.5;
  min-height: 100vh;
}

/* Page Wrapper - Sticky Footer Layout */
.page-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1; /* Chiếm hết không gian còn lại */
}
```

**Công nghệ sử dụng:**

- **CSS Variables:** Dễ dàng thay đổi theme
- **Flexbox:** Layout linh hoạt
- **Box-sizing:** Tính toán kích thước chính xác

---

### 2. Phần Header

#### a. Code HTML

```html
<header class="header" id="mainHeader">
  <div class="header-container">
    <!-- Logo -->
    <a href="index.html" class="logo">
      <span class="logo-icon">☕</span>
      <span>Kvone Coffee</span>
    </a>

    <!-- Navigation -->
    <nav class="nav" id="mainNav">
      <a href="index.html" class="nav-link active">Menu</a>
      <a href="favorites.html" class="nav-link">Yêu thích</a>
      <a href="orders.html" class="nav-link">Đơn hàng</a>
    </nav>

    <!-- Header Actions -->
    <div class="header-actions">
      <!-- Cart Button -->
      <a href="cart.html" class="cart-btn">
        🛒
        <span class="cart-badge" style="display: none">0</span>
      </a>

      <!-- User Menu / Auth Links -->
      <div class="user-menu" id="userMenu" style="display: none">
        <div class="avatar">U</div>
        <span class="user-name">User</span>
      </div>

      <!-- Mobile Menu Button -->
      <button class="mobile-menu-btn btn btn-ghost">☰</button>
    </div>
  </div>
</header>
```

**Công nghệ:**

- **Semantic HTML:** `<header>`, `<nav>` giúp SEO
- **Emoji Icons:** Không cần font icons, giảm HTTP requests

#### b. Code CSS

```css
/* File: css/layout.css */

.header {
  position: sticky;
  top: 0;
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(20px); /* Glassmorphism */
  -webkit-backdrop-filter: blur(20px);
  z-index: 200;
  transition: all var(--transition-normal);
}

.header.scrolled {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.header-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 1rem 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
}

/* Logo */
.logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-family: var(--font-display);
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--color-dark);
  text-decoration: none;
}

/* Cart Badge - Animated */
.cart-badge {
  position: absolute;
  top: -6px;
  right: -6px;
  min-width: 22px;
  height: 22px;
  padding: 0 6px;
  background: linear-gradient(135deg, #6b4a3a, #54372b);
  color: white;
  font-size: 11px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: pulse-glow 2s infinite;
}

@keyframes pulse-glow {
  0%,
  100% {
    box-shadow: 0 0 20px rgba(201, 168, 108, 0.4);
  }
  50% {
    box-shadow: 0 0 40px rgba(201, 168, 108, 0.6);
  }
}

/* Responsive */
@media (max-width: 768px) {
  .nav {
    position: fixed;
    top: 75px;
    left: 1rem;
    right: 1rem;
    flex-direction: column;
    background: white;
    border-radius: 1.5rem;
    opacity: 0;
    visibility: hidden;
    transition: all 300ms;
  }

  .nav.active {
    opacity: 1;
    visibility: visible;
  }
}
```

**Công nghệ CSS nổi bật:**

- **Sticky Positioning:** Header cố định khi scroll
- **Backdrop Filter (Glassmorphism):** Hiệu ứng kính mờ cao cấp
- **CSS Animation:** Badge nhấp nháy
- **Mobile-first Responsive:** Media queries cho màn hình nhỏ

---

### 3. Phần Banner (Hero Section)

#### a. Code HTML

```html
<section class="hero">
  <div class="hero-container">
    <span class="hero-badge">✨ Chất lượng hàng đầu</span>

    <h1 class="hero-title">
      Khởi đầu ngày mới với<br />
      <span class="hero-title-accent">ly cà phê hoàn hảo</span>
    </h1>

    <p class="hero-subtitle">
      Nơi mỗi ly cà phê là một tác phẩm nghệ thuật, được pha chế với tình yêu và
      sự tận tâm.
    </p>

    <div class="hero-actions">
      <a href="#products" class="btn btn-primary btn-lg">☕ Xem Menu</a>
      <a href="favorites.html" class="btn btn-outline btn-lg">💕 Yêu thích</a>
    </div>
  </div>
</section>
```

#### b. Code CSS

```css
/* File: css/layout.css */

.hero {
  background: url("../menu/banner.png") center/cover no-repeat;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  position: relative;
}

.hero-container {
  max-width: 900px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}

.hero-badge {
  display: inline-flex;
  padding: 0.5rem 1.25rem;
  background: rgba(201, 168, 108, 0.2);
  border: 1px solid rgba(201, 168, 108, 0.3);
  border-radius: 9999px;
  color: var(--color-secondary);
  font-size: 0.875rem;
  margin-bottom: 1.5rem;
  animation: slideUp 0.6s ease;
}

.hero-title {
  font-family: var(--font-display);
  font-size: clamp(1.75rem, 5vw, 3.5rem);
  font-weight: 700;
  color: white;
  line-height: 1.1;
  animation: slideUp 0.6s ease 0.1s both;
}

.hero-title-accent {
  background: linear-gradient(135deg, #f7e1bc 0%, #fff0d6 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

**Công nghệ:**

- **Background Image:** Relative path `../menu/banner.png`
- **Gradient Text:** Webkit clip cho hiệu ứng chữ gradient
- **Clamp():** Font size responsive tự động
- **CSS Keyframes:** Animation slideUp

---

### 4. Phần Danh sách sản phẩm (Products Section)

#### a. Code HTML

```html
<section class="section" id="products">
  <div class="container">
    <div class="section-header">
      <h2 class="section-title">Menu Đặc Biệt</h2>
    </div>

    <!-- Category Tabs (Rendered by JS) -->
    <div class="category-tabs" id="categoryTabs"></div>

    <!-- Search & Filter -->
    <div class="products-controls">
      <input
        type="search"
        class="form-input"
        placeholder="Tìm kiếm..."
        id="searchInput"
      />
      <select class="form-select" id="priceSort">
        <option value="">Sắp xếp giá</option>
        <option value="asc">Giá tăng dần</option>
        <option value="desc">Giá giảm dần</option>
      </select>
    </div>

    <!-- Product Grid (Rendered by JS) -->
    <div class="product-grid" id="productGrid"></div>
  </div>
</section>
```

#### b. Code CSS

```css
/* File: css/layout.css */

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

/* File: css/components.css */

.product-card {
  position: relative;
  background: white;
  border-radius: 1.5rem;
  overflow: hidden;
  transition: all 300ms;
  border: 1px solid rgba(84, 55, 43, 0.1);
  cursor: pointer;
}

.product-card:hover {
  transform: translateY(-12px) scale(1.02);
  box-shadow: 0 24px 64px rgba(26, 18, 9, 0.2);
}

.product-card-image {
  height: 220px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(180deg, #fff8ee, #f7e1bc);
  font-size: 100px;
}

.product-card-name {
  font-family: var(--font-display);
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--color-dark);
}

.product-card-price {
  font-size: 1.5rem;
  font-weight: 800;
  background: linear-gradient(135deg, #6b4a3a, #54372b);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

**Công nghệ:**

- **CSS Grid:** Layout tự động điều chỉnh số cột
- **Auto-fill & Minmax:** Responsive không cần media queries
- **Transform & Scale:** Hiệu ứng hover mượt mà

---

### 5. Hiệu ứng JavaScript

#### a. Header Glass Effect (Hiệu ứng kính mờ khi cuộn)

**File:** `js/enhancements.js`

```javascript
const HeaderGlass = {
  init() {
    const header = document.querySelector(".header");
    header.classList.add("glass-enhanced");

    window.addEventListener(
      "scroll",
      () => {
        if (window.scrollY > 10) {
          header.classList.add("scrolled");
        } else {
          header.classList.remove("scrolled");
        }
      },
      { passive: true }
    );
  },
};
```

**Mô tả:** Khi cuộn trang xuống > 10px, header thêm class `scrolled` để hiển thị đổ bóng.

---

#### b. Ripple Effect (Hiệu ứng gợn sóng khi click)

**File:** `js/enhancements.js`

```javascript
const RippleEffect = {
  init() {
    document.addEventListener(
      "click",
      (e) => {
        const target = e.target.closest(".btn");
        if (target) this.createRipple(e, target);
      },
      { capture: true }
    ); // Capture phase để bypass stopPropagation
  },

  createRipple(e, element) {
    const rect = element.getBoundingClientRect();
    const size = Math.max(rect.width, rect.height);
    const x = e.clientX - rect.left - size / 2;
    const y = e.clientY - rect.top - size / 2;

    const ripple = document.createElement("span");
    ripple.className = "ripple";
    ripple.style.width = `${size}px`;
    ripple.style.height = `${size}px`;
    ripple.style.left = `${x}px`;
    ripple.style.top = `${y}px`;

    element.appendChild(ripple);
    setTimeout(() => ripple.remove(), 600);
  },
};
```

**CSS:**

```css
.ripple {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.4);
  transform: scale(0);
  animation: ripple-expand 0.6s ease-out;
  pointer-events: none;
}

@keyframes ripple-expand {
  to {
    transform: scale(4);
    opacity: 0;
  }
}
```

**Công nghệ:** Event Delegation với Capture Phase

---

#### c. 3D Card Tilt (Nghiêng thẻ 3D theo chuột)

**File:** `js/enhancements.js`

```javascript
const CardTilt = {
  init() {
    document.querySelectorAll(".card-3d").forEach((card) => {
      card.addEventListener("mousemove", (e) => this.handleMove(e, card));
      card.addEventListener("mouseleave", () => this.handleLeave(card));
    });
  },

  handleMove(e, card) {
    const rect = card.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    const percentX = (x - rect.width / 2) / (rect.width / 2);
    const percentY = (y - rect.height / 2) / (rect.height / 2);

    const rotateY = percentX * 10; // Max 10 degrees
    const rotateX = -percentY * 10;

    card.style.setProperty("--rotateX", `${rotateX}deg`);
    card.style.setProperty("--rotateY", `${rotateY}deg`);
  },

  handleLeave(card) {
    card.style.setProperty("--rotateX", "0deg");
    card.style.setProperty("--rotateY", "0deg");
  },
};
```

**CSS:**

```css
.card-3d {
  transform-style: preserve-3d;
  perspective: 1000px;
  transition: transform 250ms;
}

.card-3d:hover {
  transform: perspective(1000px) rotateX(var(--rotateX, 0deg)) rotateY(
      var(--rotateY, 0deg)
    ) scale(1.02);
}
```

**Công nghệ:** CSS Custom Properties + 3D Transforms

---

#### d. Cart Badge Animation (Badge giỏ hàng nảy)

**File:** `js/enhancements.js`

```javascript
const CartBadgeAnimation = {
  init() {
    window.addEventListener("cartUpdated", () => {
      const badge = document.querySelector(".cart-badge");
      if (badge) {
        badge.classList.remove("cart-badge-bounce");
        void badge.offsetWidth; // Force reflow
        badge.classList.add("cart-badge-bounce");
      }
    });
  },
};
```

**File:** `js/cart.js`

```javascript
function addToCart(productId, sizeId, toppingIds, quantity) {
  // ... logic thêm vào giỏ ...

  saveCart(cart);
  updateCartBadge();

  // Dispatch event để kích hoạt animation
  window.dispatchEvent(new Event("cartUpdated"));

  return { success: true, message: "Đã thêm vào giỏ!" };
}
```

**CSS:**

```css
.cart-badge-bounce {
  animation: badge-bounce 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

@keyframes badge-bounce {
  0%,
  100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.3);
  }
}
```

**Công nghệ:** Custom Events để giao tiếp giữa modules

---

#### e. Debounce Search (Tìm kiếm với delay)

**File:** `js/app.js`

```javascript
function debounce(func, delay) {
  let timeout;
  return function (...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), delay);
  };
}
```

**Sử dụng trong index.html:**

```javascript
const handleSearch = debounce(function (query) {
  const products = searchProducts(query);
  renderProducts(productGrid, products);
}, 300); // Chờ 300ms sau khi user ngừng gõ
```

**Công nghệ:** Closure Pattern để tối ưu performance

---

#### f. Skeleton Loading (Khung xương khi tải dữ liệu)

**File:** `js/products.js`

```javascript
function renderSkeletons(container, count = 8) {
  container.innerHTML = Array(count)
    .fill(0)
    .map(
      () => `
    <div class="skeleton-card">
      <div class="skeleton skeleton-image"></div>
      <div class="skeleton-content">
        <div class="skeleton skeleton-text skeleton-title"></div>
        <div class="skeleton skeleton-text" style="width: 60%;"></div>
      </div>
    </div>
  `
    )
    .join("");
}
```

**CSS:**

```css
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}

@keyframes shimmer {
  0% {
    background-position: -200% 0;
  }
  100% {
    background-position: 200% 0;
  }
}
```

---

## B. TRANG CON (product-detail.html)

### 6. Bố cục chính

#### a. Code HTML

```html
<!DOCTYPE html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <title>Chi tiết sản phẩm - Kvone Coffee</title>
    <link rel="stylesheet" href="css/main.css" />
  </head>
  <body>
    <div class="page-wrapper">
      <!-- Header (giống trang chủ) -->
      <header class="header">...</header>

      <!-- Main Content -->
      <main class="main-content">
        <div class="container">
          <!-- Breadcrumb -->
          <div style="padding: 1rem 0">
            <a href="index.html">← Quay lại menu</a>
          </div>

          <!-- Product Detail (Rendered by JS) -->
          <div class="product-detail" id="productDetail"></div>
        </div>
      </main>

      <!-- Footer (giống trang chủ) -->
      <footer class="footer">...</footer>
    </div>

    <!-- JavaScript -->
    <script src="js/storage.js"></script>
    <script src="js/builder.js"></script>
    <!-- ... -->
  </body>
</html>
```

#### b. Code CSS định dạng chung

```css
/* File: css/layout.css (custom cho product-detail) */

.product-detail {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  margin-top: 2rem;
}

@media (max-width: 768px) {
  .product-detail {
    grid-template-columns: 1fr;
  }
}
```

---

### 7. Phần Product Detail (Chi tiết sản phẩm)

#### a. Code HTML (Rendered by JavaScript)

```javascript
// File: product-detail.html (inline script)
function renderProductDetail(productId) {
  const product = getProductById(productId);
  const container = document.getElementById("productDetail");

  container.innerHTML = `
    <!-- Hình ảnh -->
    <div class="product-detail-image">
      ${product.image}
      <button class="favorite-btn ${isFavorite(product.id) ? "active" : ""}"
              onclick="toggleFavorite('${product.id}')">
        ${isFavorite(product.id) ? "❤️" : "🤍"}
      </button>
    </div>
    
    <!-- Thông tin & Tùy chọn -->
    <div class="product-detail-info">
      <h1 class="product-detail-name">${product.name}</h1>
      <p class="product-detail-desc">${product.description}</p>
      
      <!-- Chọn Size -->
      <div class="builder-section">
        <h3>📐 Chọn Size</h3>
        <div id="sizeOptions"></div>
      </div>
      
      <!-- Chọn Topping -->
      <div class="builder-section">
        <h3>🧁 Chọn Topping</h3>
        <div id="toppingOptions"></div>
      </div>
      
      <!-- Số lượng -->
      <div class="quantity-control">
        <button onclick="handleBuilderQuantity(-1)">−</button>
        <span id="builderQuantity">1</span>
        <button onclick="handleBuilderQuantity(1)">+</button>
      </div>
      
      <!-- Nút thêm vào giỏ -->
      <button class="btn btn-primary w-full" onclick="addToCartFromBuilder()">
        🛒 Thêm vào giỏ - <span id="totalPrice">0đ</span>
      </button>
    </div>
  `;

  // Khởi tạo builder
  initBuilder(productId);
}
```

#### b. Code CSS

```css
/* File: css/layout.css */

.product-detail-image {
  position: relative;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(180deg, #fff8ee, #f7e1bc);
  border-radius: 1.5rem;
  font-size: 200px;
}

.favorite-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: white;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-size: 1.25rem;
  transition: all 300ms;
}

.favorite-btn.active {
  color: #e74c3c;
  animation: heartBeat 0.5s ease;
}

@keyframes heartBeat {
  0%,
  100% {
    transform: scale(1);
  }
  25% {
    transform: scale(1.3);
  }
  50% {
    transform: scale(1);
  }
  75% {
    transform: scale(1.2);
  }
}
```

---

### 10. Hiệu ứng JavaScript (Trang con)

#### a. Dynamic Price Calculation (Tính giá động)

**File:** `js/builder.js`

```javascript
function updatePriceDisplay() {
  const product = getProductById(currentProductId);
  let total = product.price;

  // Cộng giá size
  if (selectedSize) {
    const size = getSizeById(selectedSize);
    total += size.priceAdd;
  }

  // Cộng giá topping
  selectedToppings.forEach((toppingId) => {
    const topping = getToppingById(toppingId);
    total += topping.price;
  });

  // Nhân số lượng
  total *= quantity;

  // Cập nhật UI
  document.getElementById("totalPrice").textContent = formatCurrency(total);
}
```

**Công nghệ:** Real-time calculation với event listeners

---

#### b. Size/Topping Selection (Chọn tùy chọn)

```javascript
function handleSizeSelect(sizeId) {
  selectedSize = sizeId;

  // Update UI
  document.querySelectorAll(".size-option").forEach((opt) => {
    opt.classList.toggle("selected", opt.dataset.id === sizeId);
  });

  // Tính lại giá
  updatePriceDisplay();
}

function handleToppingToggle(toppingId) {
  const index = selectedToppings.indexOf(toppingId);

  if (index > -1) {
    selectedToppings.splice(index, 1); // Remove
  } else {
    selectedToppings.push(toppingId); // Add
  }

  updatePriceDisplay();
}
```

---

#### c. Add to Cart from Builder

```javascript
function addToCartFromBuilder() {
  const result = addToCart(
    currentProductId,
    selectedSize,
    selectedToppings,
    quantity
  );

  if (result.success) {
    showNotification(result.message, "success");

    // Animate cart badge
    window.dispatchEvent(new Event("cartUpdated"));
  }
}
```

---

## TỔNG KẾT CÔNG NGHỆ

### Front-end Architecture

- **Pure Vanilla JavaScript:** Không dependencies, tải nhanh
- **Modular CSS:** Dễ bảo trì, mở rộng
- **LocalStorage:** Không cần backend cho prototype

### Performance Optimizations

- **Event Delegation:** Giảm số lượng event listeners
- **DocumentFragment:** Giảm reflow khi render danh sách
- **Debounce/Throttle:** Tối ưu search và scroll
- **Lazy Loading:** Ảnh chỉ tải khi cần với `loading="lazy"`

### Browser Compatibility

- **Modern Browsers:** Chrome, Edge, Firefox, Safari (versions mới nhất)
- **CSS Features:** Grid, Flexbox, Custom Properties, Backdrop Filter
- **JavaScript:** ES6+ (Arrow functions, Template literals, Destructuring)

---

**KẾT LUẬN:** Website sử dụng công nghệ web chuẩn, không phụ thuộc framework nặng, tối ưu cho performance và dễ dàng deploy trên hosting tĩnh như Netlify.
