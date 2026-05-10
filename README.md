<html lang="es">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Tienda Credits</title>

<style>

body{
background:#0a0a0a;
color:white;
font-family:Arial;
padding:20px;
margin:0;
}

h1{
text-align:center;
margin-bottom:30px;
}

#loginBox,
#panel{
max-width:1200px;
margin:auto;
}

.card{
background:#111;
border:1px solid #333;
padding:15px;
border-radius:15px;
margin-bottom:20px;
}

input{
width:100%;
padding:12px;
margin-bottom:10px;
background:#111;
color:white;
border:1px solid #444;
border-radius:10px;
}

button{
padding:12px 20px;
border:none;
border-radius:10px;
background:#00ff88;
color:black;
font-weight:bold;
cursor:pointer;
margin:5px;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
}

.product{
background:#111;
border:1px solid #333;
border-radius:15px;
padding:15px;
}

.product img{
width:100%;
height:200px;
object-fit:cover;
border-radius:10px;
}

.price{
font-size:22px;
color:#00ff88;
margin-top:10px;
}

.creditos{
font-size:20px;
margin-bottom:20px;
}

/* POPUPS */

.popup{
display:none;
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.8);
justify-content:center;
align-items:center;
z-index:999;
}

.popup-content{
background:#111;
border:2px solid #00ff88;
padding:30px;
border-radius:15px;
width:320px;
text-align:center;
box-shadow:0 0 20px #00ff88;
}

.cerrar{
float:right;
font-size:30px;
cursor:pointer;
color:#00ff88;
}

#precioFinal{
font-size:22px;
color:#00ff88;
margin-top:10px;
}

a{
text-decoration:none;
}

</style>

</head>
<body>

<!-- LOGIN -->

<div id="loginBox" class="card">

<h1>LOGIN</h1>

<input type="email" id="email" placeholder="Correo">

<input type="password" id="password" placeholder="Contraseña">

<button onclick="login()">
Entrar
</button>

<p id="error"></p>

</div>

<!-- PANEL -->

<div id="panel" style="display:none;">

<h1>TIENDA</h1>

<div class="card">

<div class="creditos">

<button onclick="abrirCreditos()">

💰 Créditos:
<span id="creditos">0</span>

</button>

</div>

</div>

<!-- PRODUCTOS -->

<div class="grid">

<!-- PRODUCTO -->

<div class="product">

<img src="https://i.imgur.com/0rVeh4A.png">

<h2>Spotify Premium</h2>

<p>
Cuenta premium 1 mes
</p>

<div class="price">
100 créditos
</div>

<button onclick="comprar(100)">
Comprar
</button>

<button onclick="verCaracteristicas(
'Spotify Premium',
'• 1 mes\n• Premium\n• Sin anuncios\n• Calidad alta'
)">
Características
</button>

</div>

<!-- PRODUCTO -->

<div class="product">

<img src="https://i.imgur.com/u6dF9V7.png">

<h2>Netflix UHD</h2>

<p>
Cuenta UHD 1 mes
</p>

<div class="price">
150 créditos
</div>

<button onclick="comprar(150)">
Comprar
</button>

<button onclick="verCaracteristicas(
'Netflix UHD',
'• UHD 4K\n• Perfil privado\n• 1 mes'
)">
Características
</button>

</div>

</div>

</div>

<!-- POPUP CREDITOS -->

<div id="popupCreditos" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarCreditos()">

×

</span>

<h2>RECARGAR CRÉDITOS</h2>

<p>
Actualmente tienes:
<b id="creditosActuales">0</b>
créditos
</p>

<input
type="number"
id="cantidadCreditos"
placeholder="Cantidad de créditos"
oninput="calcularPrecio()">

<p id="precioFinal">
Total: $0 COP
</p>

<button onclick="mostrarMetodos()">
RECARGAR
</button>

<div id="metodosPago" style="display:none;">

<h3>Métodos de pago</h3>

<button onclick="mostrarPago(
'NEQUI',
'Número: 3001234567'
)">
NEQUI
</button>

<button onclick="mostrarPago(
'PAYPAL',
'Correo: pagos@correo.com'
)">
PAYPAL
</button>

<button onclick="mostrarPago(
'BINANCE',
'ID: 123456789'
)">
BINANCE
</button>

<br><br>

<a
href="https://wa.me/573001234567"
target="_blank">

<button>

ENVIAR COMPROBANTE

</button>

</a>

</div>

</div>

</div>

<!-- POPUP PAGOS -->

<div id="popupPago" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarPago()">

×

</span>

<h2 id="tituloPago"></h2>

<p id="infoPago"></p>

</div>

</div>

<!-- POPUP CARACTERISTICAS -->

<div id="popupCaracteristicas" class="popup">

<div class="popup-content">

<span class="cerrar"
onclick="cerrarCaracteristicas()">

×

</span>

<h2 id="tituloProducto"></h2>

<p id="infoProducto"></p>

</div>

</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getAuth,
signInWithEmailAndPassword,
onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

import {
getFirestore,
doc,
getDoc
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

const firebaseConfig = {

apiKey: "AIzaSyC8cF8i86iqxCUIlOw1ykd_Civxl1qX2FM",
authDomain: "osting-1b3f6.firebaseapp.com",
projectId: "osting-1b3f6",
storageBucket: "osting-1b3f6.firebasestorage.app",
messagingSenderId: "1080144262727",
appId: "1:1080144262727:web:3f42a97c334adb826b2362"

};

const app = initializeApp(firebaseConfig);

const auth = getAuth(app);

const db = getFirestore(app);

window.login = async function(){

const email =
document.getElementById("email").value;

const password =
document.getElementById("password").value;

try{

await signInWithEmailAndPassword(
auth,
email,
password
);

}catch(err){

document.getElementById("error").innerHTML =
"Login incorrecto";

}

}

onAuthStateChanged(auth, async(user)=>{

if(user){

document.getElementById("loginBox").style.display =
"none";

document.getElementById("panel").style.display =
"block";

const userRef =
doc(db,"users",user.uid);

const userSnap =
await getDoc(userRef);

if(userSnap.exists()){

const datos =
userSnap.data();

document.getElementById("creditos").innerHTML =
datos.creditos || 0;

}

}

});

window.abrirCreditos = function(){

document.getElementById("popupCreditos")
.style.display = "flex";

document.getElementById("creditosActuales")
.innerHTML =
document.getElementById("creditos")
.innerHTML;

}

window.cerrarCreditos = function(){

document.getElementById("popupCreditos")
.style.display = "none";

}

window.calcularPrecio = function(){

let creditos =
parseInt(
document.getElementById(
"cantidadCreditos"
).value
) || 0;

let precioPorCredito = 50;

let total =
creditos * precioPorCredito;

document.getElementById(
"precioFinal"
).innerHTML =

"Total: $" +
total.toLocaleString() +
" COP";

}

window.mostrarMetodos = function(){

document.getElementById("metodosPago")
.style.display = "block";

}

window.comprar = function(precio){

let creditos =
parseInt(
document.getElementById("creditos")
.innerHTML
);

if(creditos < precio){

abrirCreditos();

return;

}

alert("Compra realizada");

}

window.verCaracteristicas = function(
titulo,
info
){

document.getElementById(
"popupCaracteristicas"
).style.display = "flex";

document.getElementById(
"tituloProducto"
).innerHTML = titulo;

document.getElementById(
"infoProducto"
).innerText = info;

}

window.cerrarCaracteristicas =
function(){

document.getElementById(
"popupCaracteristicas"
).style.display = "none";

}

window.mostrarPago = function(titulo,info){

document.getElementById("popupPago")
.style.display = "flex";

document.getElementById("tituloPago")
.innerHTML = titulo;

document.getElementById("infoPago")
.innerHTML = info;

}

window.cerrarPago = function(){

document.getElementById("popupPago")
.style.display = "none";

}

</script>

</body>
</html>
