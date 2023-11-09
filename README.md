<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=divice-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Shop</title>
    <style>
         @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100&display=swap');

         *{
            margin: 0;
            padding: 0;
            box-sizing: border-box;

         }

         body {
            font-family: 'Montserrat', sans-serif;
            font-weight: 200;
            color: var(--tg-theme-text-color);
            background: var(--tg-theme-bg-color);
         }

         #main {
             width: 100%;
             padding: 20px;
             text-align: center;
         }

         h1 {
            margin-top: 50px;
            margin-bottom: 10px;
         }

         img {
            width: 70px;
            margin: 30px auto;
         }

         p {
           width: 350px;
           margin: 0 auto;
         }

         button {
            border: 0;
            border-radius: 5px;
            margin-top: 50px;
            height: 60px;
            width: 200px;
            font-size: 20px;
            font-weight: 500;
            cursor: pointer;
            transition: all 500ms ease;
            color: var(--tg-theme-button-color);
            background: var(--tg-theme-button-text-color);
         }

         button:hover {
            background: var(--tg-theme-secondary-bg-color);
         }

         #form {
            display: none;
            text-align: center;
         }

         input {
            width: 90%;
            outline: none;
            margin: 10px 5%;
            padding: 15px 10px;
            font-size: 14px;
            border: 2px solid silver;
            border-radius: 5px;
         }

         input:focus {
            border-color: #db5d5d;
         }
</style>
</head>
<body>
    <div id = "main">
        <h1>Онлайн магазин</h1>
        <img src="https://cdn-icons-png.flaticon.com/512/3595/3595455.png">
        <button id="buy">Купить</button>
    </div>
    <form id="form">
        <input type="text" placeholder="Имя" id="user_name">
        <input type="text" placeholder="Email" id="user_email">
        <input type="text" placeholder="Телефон" id="user_phone">
        <button id="order">Оформить</button>
    </form>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        let tg = window.Telegram.WebApp;
        let buy = document.getElementById("buy");
        let order = document.getElementById("order");
        tg.expand();

        buy.addEventListener("click", () => {
            document.getElementById("main").style.display = "none";
            document.getElementById("form").style.display = "block";
            document.getElementById("user_name").value = tg.initDataUnsafe.user.first_name + "  " + tg.initDataUnsafe.user.last_name;
        });

        order.addEventListener("click", () => {
            tg.close();
        });
    </script>
</body>
</html>
