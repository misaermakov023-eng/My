<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Миша Ермаков Exchange</title>

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>

<style>

body{
margin:0;
font-family:Arial;
background:#0f172a;
color:white;
}

header{
background:#020617;
padding:15px;
font-size:22px;
text-align:center;
}

.container{
max-width:1000px;
margin:auto;
padding:20px;
}

.card{
background:#1e293b;
padding:20px;
border-radius:10px;
margin-bottom:20px;
}

input,select,button{
padding:10px;
margin:5px;
border-radius:6px;
border:none;
}

button{
background:#3b82f6;
color:white;
cursor:pointer;
}

button:hover{
background:#2563eb;
}

.balance{
font-size:20px;
margin-top:10px;
}

.ad{
background:#111827;
padding:20px;
text-align:center;
border-radius:10px;
}

.admin{
display:none;
margin-top:15px;
}

#map{
height:300px;
border-radius:10px;
}

</style>
</head>

<body>

<header>💱 Миша Ермаков Exchange</header>

<div class="container">

<div class="card">

<h2>👤 Аккаунт</h2>

<input id="username" placeholder="Имя">
<input id="password" type="password" placeholder="Пароль">

<button onclick="register()">Регистрация</button>
<button onclick="login()">Войти</button>

<p id="userStatus"></p>

<div class="balance">
Баланс: <span id="balance">0</span> USD
</div>

</div>

<div class="card">

<h2>💱 Обмен валют</h2>

<input type="number" id="amount" placeholder="Сумма">

<select id="from">
<option>USD</option>
<option>EUR</option>
<option>RUB</option>
</select>

<select id="to">
<option>EUR</option>
<option>USD</option>
<option>RUB</option>
</select>

<button onclick="exchange()">Обменять</button>

<p id="result"></p>

</div>

<div class="card ad">

<h2>📢 Реклама</h2>

<p id="adText">Ваша реклама может быть здесь</p>

</div>

<div class="card">

<h2>🏦 Наши офисы</h2>

<div id="map"></div>

</div>

<div class="card">

<h2>🔐 Админ-панель</h2>

<input id="adminPass" type="password" placeholder="Пароль">

<button onclick="adminLogin()">Войти</button>

<div class="admin" id="adminPanel">

<h3>Изменить рекламу</h3>

<input id="newAd">
<button onclick="changeAd()">Сохранить</button>

<h3>Изменить баланс</h3>

<input type="number" id="newBalance">
<button onclick="setBalance()">Сохранить</button>

</div>

</div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

let balance = 0
let currentUser = null

function register(){

let user = document.getElementById("username").value
let pass = document.getElementById("password").value

if(!user || !pass){
alert("Введите данные")
return
}

localStorage.setItem("user_"+user, pass)
localStorage.setItem("balance_"+user, 1000)

alert("Аккаунт создан")

}

function login(){

let user = document.getElementById("username").value
let pass = document.getElementById("password").value

let saved = localStorage.getItem("user_"+user)

if(saved === pass){

currentUser = user

balance = parseFloat(localStorage.getItem("balance_"+user))

document.getElementById("balance").innerText = balance

document.getElementById("userStatus").innerText = "Вы вошли: "+user

}else{

alert("Неверный логин")

}

}

function exchange(){

if(!currentUser){
alert("Войдите в аккаунт")
return
}

let amount = parseFloat(document.getElementById("amount").value)

if(!amount || amount<=0){
alert("Введите сумму")
return
}

if(amount > balance){
alert("Недостаточно средств")
return
}

let from = document.getElementById("from").value
let to = document.getElementById("to").value

let rate = 1

if(from=="USD" && to=="EUR") rate = 0.9
if(from=="EUR" && to=="USD") rate = 1.1
if(from=="USD" && to=="RUB") rate = 90
if(from=="RUB" && to=="USD") rate = 0.011
if(from=="EUR" && to=="RUB") rate = 100
if(from=="RUB" && to=="EUR") rate = 0.01

let result = amount * rate

balance -= amount

localStorage.setItem("balance_"+currentUser, balance)

document.getElementById("balance").innerText = balance

document.getElementById("result").innerText =
"Получено: "+result.toFixed(2)+" "+to

}

function adminLogin(){

let pass = document.getElementById("adminPass").value

if(pass === "QWERTY12345"){

document.getElementById("adminPanel").style.display="block"

}else{

alert("Неверный пароль")

}

}

function changeAd(){

let text = document.getElementById("newAd").value

document.getElementById("adText").innerText = text

}

function setBalance(){

balance = parseFloat(document.getElementById("newBalance").value)

document.getElementById("balance").innerText = balance

if(currentUser){

localStorage.setItem("balance_"+currentUser,balance)

}

}

let map = L.map('map').setView([48.8566, 2.3522], 12)

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{
maxZoom:19
}).addTo(map)

L.marker([48.8566,2.3522]).addTo(map)
.bindPopup("Главный офис")

L.marker([48.86,2.29]).addTo(map)
.bindPopup("Филиал")

</script>

</body>
</html>
