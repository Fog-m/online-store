# online-store
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Онлайн-магазин TechStore</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
        }
        
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 1rem;
            text-align: center;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .products {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .product-card {
            background: white;
            border-radius: 10px;
            padding: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }
        
        .product-card:hover {
            transform: translateY(-5px);
        }
        
        .product-image {
            width: 100%;
            height: 200px;
            background-color: #ddd;
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
        }
        
        .product-title {
            font-weight: bold;
            margin: 10px 0;
        }
        
        .product-price {
            color: #667eea;
            font-size: 1.2rem;
            font-weight: bold;
        }
        
        .add-to-cart {
            background: #667eea;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
        }
        
        .cart {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin-top: 30px;
        }
        
        .cart-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🛍️ TechStore</h1>
        <p>Лучшие гаджеты по лучшим ценам</p>
    </div>
    
    <div class="container">
        <div class="products" id="products">
            <!-- Товары будут загружены через JavaScript -->
        </div>
        
        <div class="cart">
            <h2>🛒 Корзина</h2>
            <div id="cart-items"></div>
            <div id="cart-total"></div>
            <button onclick="checkout()" style="margin-top: 10px;">Оформить заказ</button>
        </div>
    </div>

    <script>
        // Данные товаров
        const products = [
            { id: 1, name: "Смартфон", price: 29990, emoji: "📱" },
            { id: 2, name: "Ноутбук", price: 59990, emoji: "💻" },
            { id: 3, name: "Наушники", price: 7990, emoji: "🎧" },
            { id: 4, name: "Часы", price: 14990, emoji: "⌚" },
            { id: 5, name: "Планшет", price: 24990, emoji: "📱" },
            { id: 6, name: "Камера", price: 39990, emoji: "📷" }
        ];

        let cart = [];

        // Отображение товаров
        function displayProducts() {
            const productsContainer = document.getElementById('products');
            productsContainer.innerHTML = products.map(product => `
                <div class="product-card">
                    <div class="product-image">${product.emoji}</div>
                    <div class="product-title">${product.name}</div>
                    <div class="product-price">${product.price.toLocaleString()} ₽</div>
                    <button class="add-to-cart" onclick="addToCart(${product.id})">
                        Добавить в корзину
                    </button>
                </div>
            `).join('');
        }

        // Добавление в корзину
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);
            
            if (existingItem) {
                existingItem.quantity++;
            } else {
                cart.push({...product, quantity: 1});
            }
            
            updateCart();
            alert(`${product.name} добавлен в корзину!`);
        }

        // Обновление корзины
        function updateCart() {
            const cartItems = document.getElementById('cart-items');
            const cartTotal = document.getElementById('cart-total');
            
            cartItems.innerHTML = cart.map(item => `
                <div class="cart-item">
                    <span>${item.emoji} ${item.name}</span>
                    <span>${item.quantity} × ${item.price.toLocaleString()} ₽</span>
                </div>
            `).join('');
            
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            cartTotal.innerHTML = `<h3>Итого: ${total.toLocaleString()} ₽</h3>`;
        }

        // Оформление заказа
        function checkout() {
            if (cart.length === 0) {
                alert('Корзина пуста!');
                return;
            }
            
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            alert(`Заказ оформлен! Сумма: ${total.toLocaleString()} ₽\nСпасибо за покупку!`);
            cart = [];
            updateCart();
        }

        // Инициализация
        displayProducts();
    </script>
</body>
</html>
