<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shop</title>
    <style>
    img {
         display: flex;
     flex-direction: column;
	     justify-content: center;
	     align-items: center;
     margin: 30px auto;
     width: 70px;
     }
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        #container {
            text-align: center;
        }

        table {
            border-collapse: collapse;
            width: 100%;
        }

        th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: center;
        }
	.form-container {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
        }

        .form-container label {
            margin-bottom: 5px;
        }

        .form-container input {
            margin-bottom: 10px;
        }
    </style>
 
</head>
<body>
    <div id="container">
        <h1>Онлайн магазин</h1>
        <div id="imageContainer">
            <img id="myImage" src="Pizza.png" alt="Картинка">
        </div>
       
       <table id="myTable" style="display: none;">
             <tbody>
                <tr>
                    <td>
                        <img src="Блины.jpeg" alt="Блины">
			<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
 <span class="total-price">0 руб.</span>
                        <span class="quantity">0</span>
                    </td>
                    <td>
                        <img src="Бургер.jpeg" alt="Бургер">
<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
 <span class="total-price">0 руб.</span>
                        <span class="quantity">0</span>
                    </td>
                </tr>
                <tr>
                    <td>
                        <img src="Курица.jpeg" alt="Курица">
<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
 <span class="total-price">0 руб.</span>
                        <span class="quantity">0</span>
                    </td>
                    <td>
                        <img src="Рыба.jpg" alt="Рыба">
<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
                        <span class="quantity">0</span>
<span class="total-price">0 руб.</span>
                    </td>
                </tr>
                <tr>
                    <td>
                        <img src="Фрукты.jpeg" alt="Фрукты">
<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
 <span class="total-price">0 руб.</span>
                        <span class="quantity">0</span>
                    </td>
                    <td>
                        <img src="Яйцо.jpg" alt="Яйцо">
<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
<span class="total-price">0 руб.</span>
                        <span class="quantity">0</span>
                    </td>
                </tr>
                <tr>
                    <td>
                        <img src="Мясо.jpg" alt="Мясо">
<span class="price">100 руб.</span>
                        <button onclick="changeQuantity(this, 1)">+</button>
                        <button onclick="changeQuantity(this, -1)">-</button>
 <span class="total-price">0 руб.</span>
                        <span class="quantity">0</span>
                    </td>
                </tr>
            </tbody>
        </table>
	 <button id="showButton" onclick="showTable()">Купить</button>
        <button id="addToCartButton" style="display: none;" onclick="addToCart()">Добавить в корзину</button>
    </div>
   <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>

        function showTable() {
            var table = document.getElementById("myTable");
            var button = document.getElementById("showButton");
	    var image = document.getElementById("myImage");	
            var addToCartButton = document.getElementById("addToCartButton");
            table.style.display = "table";
            button.style.display = "none";
	    image.style.display = "none";
            addToCartButton.style.display = "inline-block";
        }
       function changeQuantity(element, value) {
    var quantityElement = element.parentNode.querySelector('.quantity');
    var quantity = parseInt(quantityElement.innerText);
    quantity += value;
    if (quantity >= 0) {
        quantityElement.innerText = quantity.toString();
        updateTotalPrice(element.parentNode);
    }
}

function updateTotalPrice(row) {
    var quantityElement = row.querySelector('.quantity');
    var priceElement = row.querySelector('.price');
    var quantity = parseInt(quantityElement.innerText);
    var price = parseInt(priceElement.innerText);
    var totalPriceElement = row.querySelector('.total-price');
    var totalPrice = quantity * price;
    totalPriceElement.innerText = totalPrice + ' руб.';
}

         function addToCart() {
            var formContainer = document.createElement("div");
            formContainer.id = "formContainer";

            var nameLabel = document.createElement("label");
            nameLabel.textContent = "Имя:";
            var nameInput = document.createElement("input");
            nameInput.type = "text";
            nameInput.name = "name";
            formContainer.appendChild(nameLabel);
            formContainer.appendChild(nameInput);

            var addressLabel = document.createElement("label");
            addressLabel.textContent = "Адрес:";
            var addressInput = document.createElement("input");
            addressInput.type = "text";
            addressInput.name = "address";
            formContainer.appendChild(addressLabel);
            formContainer.appendChild(addressInput);

            var phoneLabel = document.createElement("label");
            phoneLabel.textContent = "Номер телефона:";
            var phoneInput = document.createElement("input");
            phoneInput.type = "text";
            phoneInput.name = "phone";
            formContainer.appendChild(phoneLabel);
            formContainer.appendChild(phoneInput);

            var submitButton = document.createElement("button");
            submitButton.textContent = "Отправить";
            submitButton.onclick = sendOrder;
            formContainer.appendChild(submitButton);

            // Вставляем форму после кнопки "Добавить в корзину"
	    var table = document.getElementById("myTable");
            var addToCartButton = document.getElementById("addToCartButton");
	    table.style.display = "none";
            addToCartButton.style.display = "none";
            addToCartButton.insertAdjacentElement("afterend", formContainer);
        }

        // Функция для отправки заказа в телеграм-бота
        function sendOrder() {
            var name = document.querySelector("input[name='name']").value;
            var address = document.querySelector("input[name='address']").value;
            var phone = document.querySelector("input[name='phone']").value;

            var table = document.getElementById("myTable");
            var rows = table.getElementsByTagName("tr");
            var data = [];

            // Проходимся по каждой строке таблицы, кроме заголовков
            for (var i = 1; i < rows.length; i++) {
                var cells = rows[i].getElementsByTagName("td");
                var productName = cells[0].querySelector("img").alt;
                var price = cells[0].querySelector(".price").innerText;
                var quantity = cells[0].querySelector(".quantity").innerText;
                var totalPrice = cells[0].querySelector(".total-price").innerText;

                // Создаем объект с данными товара
                var productData = {
                    name: productName,
                    price: price,
                    quantity: quantity,
                    totalPrice: totalPrice
                };

                // Добавляем объект в массив данных
                data.push(productData);
            }

            // Отправляем данные заказа и контактные данные в телеграм-бота
            axios.post('https://api.telegram.org/bot<YOUR_BOT_TOKEN>/sendMessage', {
                chat_id: '<CHAT_ID>',
                text: 'Заказ:\n' + JSON.stringify(data, null, 2) + '\n\n' +
                      'Имя: ' + name + '\n' +
                      'Адрес: ' + address + '\n' +
                      'Номер телефона: ' + phone
            })
            .then(function (response) {
                console.log('Заказ успешно отправлен в телеграм-бота');
		tg.close();
            })
            .catch(function (error) {
                console.error('Ошибка при отправке заказа в телеграм-бота', error);
            });
	    
        }

    </script>
</body>
</html>
