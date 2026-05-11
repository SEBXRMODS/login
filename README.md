<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tienda Sebxr Mods</title>

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
max-height:90vh;
overflow:auto;
}

.cerrar{
float:right;
font-size:30px;
cursor:pointer;
color:#00ff88;
}

</style>
</head>
<body>

<div id="loginBox" class="card">

<h1>LOGIN / REGISTRO</h1>

<input type="email" id="email" placeholder="Correo">

<input type="password" id="password" placeholder="Contraseña">

<button onclick="login()">
Entrar o Registrarse
</button>

<p id="error"></p>

</div>

<div id="panel" style="display:none;">

<h1>TIENDA SEBXR MODS</h1>

<div class="card">

<h2>
💰 Créditos:
<span id="creditos">0</span>
</h2>

<button onclick="abrirCreditos()">
Recargar Créditos
</button>

</div>

<div class="grid">

<div class="product">

<!-- CAMBIAR IMAGEN -->
<img src="https://i.imgur.com/0rVeh4A.png">

<!-- CAMBIAR NOMBRE -->
<h2>Panel Sebxr Mods</h2>

<!-- CAMBIAR DESCRIPCION -->
<p>Panel premium sin blacklist</p>

<button onclick="abrirDuraciones('Panel Sebxr Mods')">
Comprar
</button>

</div>

<div class="product">

<img src="https://i.imgur.com/u6dF9V7.png">

<h2>Netflix UHD</h2>

<p>Cuenta UHD privada</p>

<button onclick="abrirDuraciones('Netflix UHD')">
Comprar
</button>

</div>

</div>

</div>

<!-- POPUP CREDITOS -->

<div id="popupCreditos" class="popup">
<div class="popup-content">

<span class="cerrar" onclick="cerrarCreditos()">×</span>

<h2>RECARGAR</h2>

<input type="number" id="cantidadCreditos" placeholder="Cantidad créditos" oninput="calcularPrecio()">

<p id="precioFinal">Total: $0 COP</p>

<button onclick="mostrarMetodos()">
Continuar
</button>

<div id="metodosPago" style="display:none;">

<!-- CAMBIAR DATOS -->

<button onclick="mostrarPago('NEQUI','3001234567')">
NEQUI
</button>

<button onclick="mostrarPago('PAYPAL','correo@paypal.com')">
PAYPAL
</button>

<br><br>

<!-- CAMBIAR WHATSAPP -->

<a href="https://wa.me/573001234567" target="_blank">

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

<span class="cerrar" onclick="cerrarPago()">×</span>

<h2 id="tituloPago"></h2>

<p id="infoPago"></p>

</div>
</div>

<!-- POPUP DURACIONES -->

<div id="popupDuraciones" class="popup">
<div class="popup-content">

<span class="cerrar" onclick="cerrarDuraciones()">×</span>

<h2 id="tituloDuracion"></h2>

<button onclick="seleccionarDuracion('1 Día',20)">
1 Día - 20 créditos
</button>

<button onclick="seleccionarDuracion('7 Días',80)">
7 Días - 80 créditos
</button>

<button onclick="seleccionarDuracion('1 Mes',150)">
1 Mes - 150 créditos
</button>

<button onclick="seleccionarDuracion('1 Año',1000)">
1 Año - 1000 créditos
</button>

</div>
</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getAuth,
signInWithEmailAndPassword,
createUserWithEmailAndPassword,
onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

import {
getFirestore,
doc,
getDoc,
setDoc,
updateDoc,
collection,
addDoc
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

// FIREBASE

const firebaseConfig = {

apiKey: "TU_API_KEY",

authDomain: "TU_AUTH_DOMAIN",

projectId: "TU_PROJECT_ID",

storageBucket: "TU_STORAGE_BUCKET",

messagingSenderId: "TU_SENDER_ID",

appId: "TU_APP_ID"

};

const app = initializeApp(firebaseConfig);

const auth = getAuth(app);

const db = getFirestore(app);

// GENERADOR KEYS

function generarKey(){

const chars =
"ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";

let key = "SEBXR-";

for(let i=0;i<4;i++){

key += chars.charAt(
Math.floor(Math.random()*chars.length)
);

}

key += "-";

for(let i=0;i<4;i++){

key += chars.charAt(
Math.floor(Math.random()*chars.length)
);

}

return key;

}

// EXPIRACION

function calcularExpiracion(dias){

const fecha = new Date();

fecha.setDate(
fecha.getDate()+dias
);

return fecha.toISOString();

}

// LOGIN / REGISTRO

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

try{

await createUserWithEmailAndPassword(
auth,
email,
password
);

}catch(error){

document.getElementById(
"error"
).innerHTML = error.message;

}

}

}

// SESION

onAuthStateChanged(auth, async(user)=>{

if(user){

loginBox.style.display = "none";

panel.style.display = "block";

const userRef =
doc(db,"users",user.uid);

const userSnap =
await getDoc(userRef);

if(!userSnap.exists()){

await setDoc(userRef,{

email:user.email,

uid:user.uid,

creditos:0

});

}

const nuevoSnap =
await getDoc(userRef);

const datos =
nuevoSnap.data();

creditos.innerHTML =
datos.creditos || 0;

}

});

// CREDITOS

window.abrirCreditos = function(){

popupCreditos.style.display =
"flex";

}

window.cerrarCreditos = function(){

popupCreditos.style.display =
"none";

}

// PRECIO

window.calcularPrecio = function(){

let c =
parseInt(
cantidadCreditos.value
)||0;

let total = c * 50;

precioFinal.innerHTML =

"Total: $" +

total.toLocaleString() +

" COP";

}

// METODOS

window.mostrarMetodos = function(){

metodosPago.style.display =
"block";

}

// PAGO

window.mostrarPago = function(
titulo,
info
){

popupPago.style.display =
"flex";

tituloPago.innerHTML =
titulo;

infoPago.innerHTML =
info;

}

window.cerrarPago = function(){

popupPago.style.display =
"none";

}

// DURACIONES

window.abrirDuraciones = function(
prod
){

popupDuraciones.style.display =
"flex";

tituloDuracion.innerHTML =
prod;

}

window.cerrarDuraciones =
function(){

popupDuraciones.style.display =
"none";

}

// COMPRAR

window.seleccionarDuracion =
async function(
duracion,
precio
){

const user =
auth.currentUser;

if(!user)return;

let creditosActuales =
parseInt(
creditos.innerHTML
);

if(creditosActuales < precio){

cerrarDuraciones();

abrirCreditos();

return;

}

let dias = 1;

if(duracion === "7 Días")
dias = 7;

if(duracion === "1 Mes")
dias = 30;

if(duracion === "1 Año")
dias = 365;

const nuevaKey =
generarKey();

const expiracion =
calcularExpiracion(dias);

const userRef =
doc(db,"users",user.uid);

await updateDoc(userRef,{

creditos:
creditosActuales - precio

});

await addDoc(
collection(db,"keys"),
{

key:nuevaKey,

producto:
tituloDuracion.innerHTML,

duracion:duracion,

expira:expiracion,

estado:"activa",

uid:user.uid,

email:user.email,

creada:new Date()
.toISOString(),

dispositivo:
navigator.userAgent

});

creditos.innerHTML =

creditosActuales - precio;

alert(

"COMPRA EXITOSA\n\nKEY:\n" +

nuevaKey

);

cerrarDuraciones();

}

</script>
</body>
</html>
