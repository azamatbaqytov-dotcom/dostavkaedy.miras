<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Мобильное Меню</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { font-family: sans-serif; background-color: #f3f4f6; margin: 0; padding-bottom: 100px; }
        .product-card { background: white; border-radius: 15px; overflow: hidden; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .btn-add { background-color: #10b981; color: white; width: 100%; padding: 10px; border-radius: 8px; font-weight: bold; border: none; }
        .cart-panel { position: fixed; bottom: 0; left: 0; right: 0; background: white; padding: 15px; border-top-left-radius: 20px; border-top-right-radius: 20px; box-shadow: 0 -5px 20px rgba(0,0,0,0.1); z-index: 100; }
        .whatsapp-btn { background-color: #25D366; color: white; width: 100%; padding: 15px; border-radius: 12px; font-size: 18px; font-weight: bold; text-align: center; display: block; border: none; text-decoration: none; }
    </style>
</head>
<body>

    <!-- Шапка -->
    <div style="background: white; padding: 15px; text-align: center; border-bottom: 1px solid #ddd;">
        <h2 style="margin: 0; color: #059669;">НАШЕ МЕНЮ</h2>
    </div>

    <!-- Список товаров -->
    <div style="padding: 15px;" id="menu">

        <!-- Меню будет вставлено скриптом -->

    </div>

    <!-- Нижняя панель (Корзина) -->
    <div class="cart-panel">
        <div id="cart-content" style="margin-bottom: 10px; font-size: 14px; max-height: 100px; overflow-y: auto;">
            Корзина пуста
        </div>
        <div style="display: flex; justify-content: space-between; font-weight: bold; margin-bottom: 10px; font-size: 18px;">
            <span>Итого:</span>
            <span id="total-price">0 ₸</span>
        </div>
        <button class="whatsapp-btn" onclick="sendToWhatsApp()">ЗАКАЗАТЬ В WHATSAPP</button>
    </div>

    <script>
        const MY_PHONE = "77762916934";
        let cart = [];

        const products = [
            {name: "Крылышки 8шт", price: 1800},
            {name: "Наггетсы", price: 1300},
            {name: "Донер стандарт", price: 1200},
            {name: "Донер полтора", price: 1300},
            {name: "Картофельные дольки", price: 1000},
            {name: "Фри", price: 800},
            {name: "Пицца Пепперони", price: 2000},
            {name: "Пицца Маргарита", price: 1800},
            {name: "Пицца 4 сезона", price: 2300},
            {name: "Пицца Сырная", price: 2300},
            {name: "Пицца Болоньезе", price: 2500}
        ];

        // Генерация карточек товаров
        const menuDiv = document.getElementById("menu");
        products.forEach((product) => {
            const card = document.createElement("div");
            card.className = "product-card";
            card.innerHTML = `
                <div style="padding: 15px;">
                    <h3 style="margin: 0 0 5px 0;">${product.name}</h3>
                    <p style="color: #6b7280; font-size: 14px;">${product.price} ₸</p>
                    <button class="btn-add" onclick="addToCart('${product.name}', ${product.price})">+ Добавить</button>
                </div>
            `;
            menuDiv.appendChild(card);
        });

        function addToCart(name, price) {
            cart.push({name, price});
            renderCart();
        }

        function renderCart() {
            const content = document.getElementById('cart-content');
            const totalDisplay = document.getElementById('total-price');
            
            if (cart.length === 0) {
                content.innerHTML = "Корзина пуста";
                totalDisplay.innerText = "0 ₸";
                return;
            }

            let html = "";
            let total = 0;
            cart.forEach((item, i) => {
                html += <div>• ${item.name} (${item.price} ₸)</div>;
                total += item.price;
            });
            
            content.innerHTML = html;
